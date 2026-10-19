# vulstr

**vulstr** is a small string toolkit for Vulpin. It adds the string helpers Vulpin doesn't have built in, written in the same compact one-letter style as Vulpin itself.

---

## Installation
Just copy `vulstr.vul` and add it to your modules

---

## Quick Start

```basic
name="  vulpin  "
? has(name.S,"pin") & sw(name.S,"vul")
    G"looks like vulpin"
;
G rv("vulpin")        # nipluv
G lp("7",3,"0")       # 007
G tr("Hello World",8) # Hello...
```

---

## Already built in

vulstr doesn't repeat what Vulpin already has:

| Built-in | Does | Example |
|----------|------|---------|
| `len(s)` | length | `len("hi")` → `2` |
| `a + b` | join two strings | `"a"+"b"` → `"ab"` |
| `s[a:b]`, `s[-1]` | slice / index | `"vulpin"[0:3]` → `"vul"` |
| `.U` `.L` | upper / lower | `"hi".U` → `"HI"` |
| `.S` | strip spaces from both ends | `" hi ".S` → `"hi"` |
| `.T` `.C` | title / capitalize | `"hi there".T` → `"Hi There"` |
| `.R(old,new)` | replace all | `"a-b".R("-","+")` → `"a+b"` |
| `.F(sub)` | first index, `-1` if missing | `"hello".F("l")` → `2` |
| `.SP` / `.SP(d)` | split on spaces / on `d` | `"a,b".SP(",")` → `["a", "b"]` |
| `sep.J(list)` | join a List | `"-".J(["a","b"])` → `"a-b"` |
| `fmt(s, ...)` | format | `fmt("{} + {}",1,2)` → `"1 + 2"` |

---

## Functions

Checks return `true` / `false`, so they work with `&` and `|`.
An argument written as `!x` is optional.

### Searching

| Function | Does | Example |
|----------|------|---------|
| `has(s,p)` | `s` contains `p` | `has("vulpin","pin")` → `true` |
| `sw(s,p)` | `s` starts with `p` | `sw("vulpin","vul")` → `true` |
| `ew(s,p)` | `s` ends with `p` | `ew("main.vul",".vul")` → `true` |
| `rf(s,p)` | last index of `p`, `-1` if missing | `rf("abcabc","bc")` → `4` |
| `fa(s,p)` | every index of `p` | `fa("banana","a")` → `[1, 3, 5]` |
| `ct(s,p)` | how many times `p` appears | `ct("banana","a")` → `3` |

### Changing

| Function | Does | Example |
|----------|------|---------|
| `rpt(s,n)` | repeat `n` times | `rpt("ab",3)` → `"ababab"` |
| `rv(s)` | reverse | `rv("vulpin")` → `"nipluv"` |
| `rn(s,o,n,k)` | replace only the first `k` of `o` with `n` | `rn("a-b-c","-","+",1)` → `"a+b-c"` |
| `ins(s,i,t)` | insert `t` at index `i` | `ins("helo",3,"l")` → `"hello"` |
| `dp(s,p)` | drop prefix `p` | `dp("unhappy","un")` → `"happy"` |
| `ds(s,p)` | drop suffix `p` | `ds("main.vul",".vul")` → `"main"` |
| `tr(s,n,!t)` | cut to `n` chars, ending in `t` (default `"..."`) | `tr("Hello World",8)` → `"Hello..."` |
| `sqz(s)` | squeeze runs of whitespace into one space | `sqz("a   b")` → `"a b"` |
| `swc(s)` | swap upper and lower case | `swc("Vulpin")` → `"vULPIN"` |
| `pt(s,d)` | split at the first `d` into `[before, d, after]` | `pt("key=value","=")` → `["key", "=", "value"]` |
| `ln(s)` | split into lines (`\n` or `\r\n`) | `ln("a\nb")` → `["a", "b"]` |
| `ch(s)` | List of characters | `ch("abc")` → `["a", "b", "c"]` |

### Trimming & padding

| Function | Does | Example |
|----------|------|---------|
| `lt(s)` | trim whitespace on the left | `lt("  hi ")` → `"hi "` |
| `rt(s)` | trim whitespace on the right | `rt("  hi ")` → `"  hi"` |
| `stc(s,c)` | strip any of the characters in `c` from both ends | `stc("--hi=-","-=")` → `"hi"` |
| `lp(s,n,!c)` | pad on the left to width `n` with `c` (default space) | `lp("7",3,"0")` → `"007"` |
| `rp(s,n,!c)` | pad on the right | `rp("ab",5,".")` → `"ab..."` |
| `ce(s,n,!c)` | center in width `n` | `ce("hi",8,"*")` → `"***hi***"` |
| `zf(s,n)` | zero fill, keeping a `-`/`+` sign in front | `zf("-42",5)` → `"-0042"` |

### Checks

| Function | True when `s` is... | Example |
|----------|---------------------|---------|
| `isd(s)` | all digits | `isd("123")` → `true` |
| `isa(s)` | all letters | `isa("abc")` → `true` |
| `isan(s)` | all letters or digits | `isan("ab12")` → `true` |
| `iss(s)` | all whitespace (and not empty) | `iss(" \t")` → `true` |
| `isb(s)` | empty or only whitespace | `isb("")` → `true` |
| `islo(s)` | has letters, none uppercase | `islo("abc1")` → `true` |
| `isup(s)` | has letters, none lowercase | `isup("ABC")` → `true` |
| `isnum(s)` | a number like `42`, `-3.5`, `.5` | `isnum("-3.5")` → `true` |
| `ispal(s)` | a palindrome (ignores case and spaces) | `ispal("Never odd or even")` → `true` |

### Converting

| Function | Does | Example |
|----------|------|---------|
| `ti(s,!d)` | Int from `s`, or `d` (default `0`) if it isn't a whole number | `ti("42")` → `42`, `ti("abc",-1)` → `-1` |
| `tf(s,!d)` | Float from `s`, or `d` (default `0.0`) | `tf("3.5")` → `3.5` |
| `od(c)` | character code (printable ASCII, else `-1`) | `od("A")` → `65` |
| `chr(n)` | character for a code (32-126, else `""`) | `chr(97)` → `"a"` |

### Comparing

| Function | Does | Example |
|----------|------|---------|
| `cmp(a,b)` | `-1`, `0` or `1` | `cmp("a","b")` → `-1` |
| `icmp(a,b)` | like `cmp`, ignoring case | `icmp("ABC","abc")` → `0` |
| `ieq(a,b)` | equal, ignoring case | `ieq("Hi","hI")` → `true` |

---

## Notes

- `od` and `chr` only cover printable ASCII (codes 32 to 126), since Vulpin has no built-in character codes.
- `lp`, `rp` and `ce` use only the first character of `c`.
- Strings shorter than the pad width are returned as they are, never cut.
