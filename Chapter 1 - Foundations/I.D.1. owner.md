- the one location (e.g. scope) is responsible for ultimately deallocating a value
- when value's owner no longer has use, it is the owner's responsibility to do any necessary cleanup for that value by "dropping" it. See [[I.D.3. dropping & drop order]]

"Are there any times where Rust does not automatically drop the value and you have to do manual clean-up?" -Joel


