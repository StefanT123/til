# Reorder models trait

Reorderable trait to change position of models in minimum number of queries
```php
trait Reorderable
{
    /**
     * Reorder items by changing the
     * value in the position field in DB.
     *
     * @param array  $data
     *
     * @return \Illuminate\Support\Collection
     */
    public function reorder(array $data)
    {
        $currentPosition = $data['currentPosition'];
        $droppedPosition = $data['droppedPosition'];
        $move = $currentPosition > $droppedPosition ? 'up' : 'down';
        $modelTable = $this->getTable();

        $this->setDraggedItemPositionToZero($currentPosition);

        if ($move === 'down') {
            \DB::statement("
                UPDATE {$modelTable}
                SET position = (position - 1)
                WHERE position > {$currentPosition}
                AND position <= {$droppedPosition}
            ");
        }

        if ($move === 'up') {
            \DB::statement("
                UPDATE {$modelTable}
                SET position = (position + 1)
                WHERE position >= {$droppedPosition}
                AND position < {$currentPosition}
            ");
        }

        $this->setDesiredPositionOnItem($droppedPosition);

        return $this->orderBy('position')->get();
    }

    /**
     * Set position to 0 to the item that is dragged.
     *
     * @param int $currentPosition
     */
    protected function setDraggedItemPositionToZero($currentPosition)
    {
        $draggedItem = $this->getDraggedItem($currentPosition);
        $draggedItem->update(['position' => 0]);
    }

    /**
     * Set the desired position for the dragged item.
     *
     * @param int $droppedPosition
     */
    protected function setDesiredPositionOnItem($droppedPosition)
    {
        $draggedItem = $this->getDraggedItem(0);
        $draggedItem->update(['position' => $droppedPosition]);
    }

    /**
     * Get model of the dragged item.
     *
     * @param int $currentPosition
     *
     * @return Illuminate\Database\Eloquent\Model
     */
    protected function getDraggedItem($currentPosition)
    {
        return $this->findByPosition($currentPosition)->first();
    }

    /**
     * Scope a query to find model by position.
     *
     * @param \Illuminate\Database\Eloquent\Builder $query
     * @param int $currentPosition
     *
     * @return \Illuminate\Database\Eloquent\Builder
     */
    public function scopeFindByPosition($query, $currentPosition)
    {
        return $query->where('position', $currentPosition);
    }
}
```
