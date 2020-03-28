# Soft deletes won't work with Query Builder

Soft-deletes will exclude entries when you use Eloquent, like `User::all()`, but won't work if you use Query Builder, like `DB::table('users')->get();`
