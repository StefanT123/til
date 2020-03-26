# Override the default reset password functionality

```php
public function build()
{
    $email = $this->user->email;

    $this->deleteExistingResetToken($email);

    $token = $this->createToken();
    \DB::table('password_resets')->insert($this->getPayload($email, $token));

    return $this->view('auth.emails.revalidate_user')->with(['token' => $token]);
}

protected function deleteExistingResetToken($email)
{
    return \DB::table('password_resets')
            ->where('email', $email)
            ->delete();
}

protected function createToken()
{
    return hash_hmac('sha256', str_random(40), env('APP_KEY'));
}

protected function getPayload($email, $token)
{
    return ['email' => $email, 'token' => bcrypt($token), 'created_at' => now()];
}
```
