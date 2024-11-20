## 디버거가 없을때

```
$ iex -S mix
iex(1)> header = << 0, 1, 0, 8, 0, 120 >>
<<0, 1, 0, 8, 0, 120>>
iex(2)> Buggy.parse_header header
format: 1
tracks: 8
** (FunctionClauseError) no function clause matching in Buggy.decode/1    
    
    The following arguments were given to Buggy.decode/1:
    
        # 1
        120
    
    Attempted function clauses (showing 2 out of 2):
    
        def decode(<<1::integer-size(1), beats::integer-size(15)>>)
        def decode(<<0::integer-size(1), fps::integer-size(7), beats::integer-size(8)>>)
    
    (buggy 0.1.0) lib/buggy.ex:14: Buggy.decode/1
    iex:2: (file)
```

## 디버거 적용

```
iex(1)> header = << 0, 1, 0, 8, 0, 120 >>
<<0, 1, 0, 8, 0, 120>>
iex(2)> Buggy.parse_header header
Break reached: Buggy.parse_header/1 (lib/buggy.ex:9)

    6:     division::integer-16,
    7:     >>
    8:   ) do
    9:     require IEx; IEx.pry
   10:     IO.puts "format: #{format}"
   11:     IO.puts "tracks: #{tracks}"
   12:     IO.puts "division: #{decode(division)}"
```