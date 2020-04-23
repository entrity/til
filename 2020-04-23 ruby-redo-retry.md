I actually learned this some months ago while working at ActionVerb (Files.com), but I had to re-learn it today:

```ruby
begin
  retries ||= 0
  ...
rescue
  retry if (retries += 1) < 3
  ...
end
```

`redo` works like `retry` but gets called in a block, not in a `rescue`
