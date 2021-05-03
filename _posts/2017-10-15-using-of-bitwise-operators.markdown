---
layout: post
title: "Using Bitwise Operators"
date: 2017-10-15
tags: programming
---

An interesting thing I learned about a couple years ago in school is bitwise operators. I honestly mostly forgot about them until a coworker pointed out an implementation in our codebase the other day. I want to talk about a couple "practical" uses for them in that I've seen.

Before we begin, let's do a quick math recap. An _operator_ is a tool that acts on the operands to produce another output. Famous operators are `+`, `-`, `*`, etc. It is both the element or tool that acts upon operands, and what we call the thing that denotes the action. An _operand_ is the object of the mathematical operation. So in `2 + 2`, the `2`s are operands, the plus sign is the operator.

## Introduction to Bitwise Operators

So what are Bitwise Operators? Well, an operator that operates on bits! Basically, they are operators that move around bits in patterns (like binary numerals) at the individual level. Because they operate at such a low level, they are general very speedy. Remember operators are just like `+`/plus and `-`/minus so they also have mathematical symbols _and_ english names. The programmatic or mathematical denotation is going to be different across languages.

I'm going to go through and explain some really common ones. Sometimes I understand code better than English so I've also just coded out in ruby what the logic _means_, but this is my own pseudocode, _not_ source code! Ok, here are the main bitwise operators:

### NOT

Also known as a complement, this operation performs negation on each bit so `1111` would become `0000`, `10101` becomes `01010`, etc. In code:

```ruby
def NOT(bit)
  output = ''
  bit.each_char do |char|
    output += char == '0' ? '1' : '0'
  end
  return output
end
```

### AND

This takes _two_ operands and multiplies each bit. So `1111 AND 0000` is `0000` (`1*0` across all bits), `10101 AND 00111` is `00101`, etc. 

`AND` reminds me of a lot of languages Boolean `||` operators when `false || true`, `true || true`, `false || false`, the bitwise `AND` acts in an identical way, but with binary. In code:

```ruby
def AND(bit_1, bit_2)
  output = ''
  bit_1.split('').zip(bit_2.split('')).each do |arr|
    output += (arr[0].to_i * arr[1].to_i).to_s
  end
  return output
end
```

### OR

This also takes _two_ operands. The `OR` takes two bit patterns and results in `0` if both bits are `0`, or else `1`. So, `1111 AND 0000` is `1111`, `10101` and `00011` is `10111`, etc.

```ruby
def OR(bit_1, bit_2)
  output = ''
  bit_1.split('').zip(bit_2.split('')).each do |arr|
    if arr[0] == '0' && arr[1] == '0'
      output += '0'
    else
      output += '1'
    end
  end
  return output
end
```

### XOR

This is our most complicated one yet. `XOR` also takes _two_ operands where the result in is 1 if only the _first_ bit is 1 _or_ only the second bit is 1, but is 0 if both are 0 or both are 1. Ah, confusing. Let's code this.

```ruby
def XOR(bit_1, bit_2)
  output = ''
  bit_1.split('').zip(bit_2.split('')).each do |arr|
    if arr[0] == arr[1]
      output += '0'
    else
      output += '1'
    end
  end
  return output
end
```

Ah, that's better.

So these operators are pretty cool! They do simple math on binary and we can kind of see how they might be useful on a theoretical level. Just like we couldn't image life without multiplication, addition, subtraction, and division, bitwise operators are essential to a computer's life. From these simple building blocks, we can make some pretty powerful math.

All programming languages I've seen have bitwise methods built it, but they look a little different than what we've defined here. For example, Ruby bitwise operators:

```bash
NOT: ~
AND: &
OR : |
XOR: ^
```

Then there are also really cool bit shifters in ruby as well: `<<` and `>>`. These shift the integers bits to the left or right by a given number of positions like

```ruby
(a >> 2).to_s(2)
```

where `a` is a decimal, `to_s(2)` means `to_binary` basically, and `>> 2` means, shift bits right 2 places. Example in `irb`:

```ruby
> a = 64
 => 64
> a.to_s(2) # the binary equivalent of a
 => "1000000"
> (a >> 2).to_s(2) # the binary equivalent of a shifted to the right
 => "10000"
```

Anyway, we could stay here all day talking about how cool shifting bits is but I  want to go into a couple cool use cases or examples I've seen of using these practically.

## Tic Tac Toe

_Note: In researching for this post I found this brilliant description of using bitwise operators in tic-tac-toe by Joris Labie: [Using bit-logic to keep track of a tic-tac-toe game](https://codepen.io/labiej/post/using-bit-logic-to-keep-track-of-a-tic-tac-toe-game). Make sure to check it out for a more detailed description of how this works!_

Building a game of tic-tac-toe is often one of the first intro level tasks a new programmer will be asked to do. It comes up often in interviews or code challenges. When I was in Ada Academy, our introduction to JavaScript was building a tic-tac-toe game in the browser. I enjoyed the project but I had a hard time formulated a good way to make the logic for winning a game. There are a lot of different possibilities for how to win across 9 different squares. Fortunately for me, I was also first learning about bitwise operators at the time, and got to thinking that `X`s and `O`s aren't all that different from `1`s and `0`s. Perhaps I could use bitwise operator logic to keep track of combinations across the board.

I knew I needed to check every move for a winning score to judge the outcome, so I wrote a method `checkEnvironment` that would call `winningScore` each turn which would determine if the player that went last successful created a winning pattern of `X`s or `O`s.

So here's how the `winningScore` logic worked. It relied on an array of `binaryWins` or 8 unique ways to win (3 horizontal, 3 vertical, 2 diagonal). These are very special numbers and taking a look at them may help to figure out why.

These are the winning combination numbers in binary:

```bash
[111, 111000, 111000000, 1001001, 10010010, 100100100, 100010001, 1010100]
```

and in decimal:

```bash
[7, 56, 448, 73, 146, 292, 273, 84]
```

And then let me express them one final way, again, in binary, but with some extraneous `0`s:

```bash
[['0', '0', '0'],
 ['0', '0', '0'],
 ['1', '1', '1']],
[['0', '0', '0'],
 ['1', '1', '1'],
 ['0', '0', '0']],
[['1', '1', '1'],
 ['0', '0', '0'],
 ['0', '0', '0']],
[['0', '0', '1'],
 ['0', '0', '1'],
 ['0', '0', '1']],
[['0', '1', '0'],
 ['0', '1', '0'],
 ['0', '1', '0']],
[['1', '0', '0'],
 ['1', '0', '0'],
 ['1', '0', '0']],
[['1', '0', '0'],
 ['0', '1', '0'],
 ['0', '0', '1']],
[['0', '0', '1'],
 ['0', '1', '0'],
 ['1', '0', '0']]
```

Look familiar? These binary numbers are an exact expression of the wins!

It might help at this point to revisit our bitwise `AND` operator, which takes two operands and returns multiplies each bit. This means if you compare any combination that a current player has across the board, with each of the binary wins, any `0` bit in the players combinations, cancels out and becomes `0`, but any place where the win's combination is `1` and the player has that `1` will register as a hit. For example, look at me winning diagonally on this board represented as a multi-dimensional array (I'm `X`):

```bash
[['X', 'O', 'X'],
 ['O', 'X', 'O'],
 ['X', 'O', 'X']]
```

And here's one of the binary wins:

```bash
[['1', '0', '0'],
 ['0', '1', '0'],
 ['0', '0', '1']]
```

If we represent each of the `X`'s on the game board as a 1, even though there are more than the three winning `X`s, they'll be canceled out by the `AND` operator if compared with our binary win!

This is pretty cool! Now that we have our logic figured out, the code is simple (excuse my javascript, it's not my primary language, but this works!):

Early on, set our binary wins:

```js
binaryWins = [7, 56, 448, 73, 146, 292, 273, 84];
```

Write our `winningScore` logic:

```js
winningScore: function(score){
  var self = this;
  for (i = 0; i < self.binaryWins.length; i += 1) {
    if ((score & self.binaryWins[i]) === self.binaryWins[i]) {
      return true;
    }
  }
  return false;
}
```

Each check we iterate through the possible wins, and use our `score` and the `win` as operands in the `AND` operator, i.e.
`score & self.binaryWins[i]` and return a boolean for if a winning score has been found.

So this is really neat. We've just used a bitwise operator for real! But tic-tac-toe is not business logic (unless you have a really cool tic-tac-toe business, please let me know if you do). Let's explore some other ways we could use these smooth operators.

## Boolean or Bitwise Logic?

So we often use boolean logic in conditionals, but bitwise logic is just as generally powerful! These conditionals are often used in assigning colors on the RGB spectrum, for example. We can also assign a range of random elements to different binary numbers and use bitwise operators to compare them. `&` and `|` do a good job comparing if two sets have an intersection. `^` can be used to see what is different between two sets. Anytime we have sets of relationships, they can be compared using bitwise logic.

## Ruby's Secure Compare

This is the `secure_compare` method in Ruby:

```ruby
def secure_compare(a, b)
  return false if a.empty? || b.empty? || a.bytesize != b.bytesize
  l = a.unpack "C#{a.bytesize}"

  res = 0
  b.each_byte { |byte| res |= byte ^ l.shift }
  res == 0
end
```

`secure_compare` is a super cool method that protects us from timing attacks, or attacks where an attacker can measure stuff about the response of a site by how long it takes to repsond. When string equality operators work left to right (i.e. `user_input == 'string'`) and a user is inputting something that controls that logic, they can execute a timing attack.

So to prevent this, `secure_compare` takes hashes of the two strings and compares those instead like:

```ruby
secure_compare(
  Digest::SHA256.hexigest('a'),
  Digest::SHA256.hexigest('b')
)
```

If we look at the code about for `secure_compare`, we can see that it steps through each letter, unpacking the byte size as it goes. It then iterates on those characters byte sizes and uses the `XOR` operator to compare them. We can see that if two of the bytes in the corresponding hashes mismatch,`res` is no longer zero and the compare returns `false`.

Each hash pasted in is of an equal length and `XOR` is used to compare and find any differences in their binary equivalents. This is not only more secure because it takes constant time to compare the hashes (no ability to measure the time differences with different inputs), but it's also really fast!

## Rails bitfields gem

Finally, I want to talk about a really cool gem, [`bitfields`](https://github.com/grosser/bitfields). It's less directly related to the operators but it uses binary logic to store things in `ActiveRecord`. 

Say you have a table, `Puppy` with multiples columns `has_chew_toy`, `likes_pets`, and `good_walker`, which are all Boolean values. That's a lot of trues and falses for one table that seems primarily based around Booleans. What if we could save _one_ integer to represent all these fields? We can!

The Boolean values are organized like:

```text
true false false => 1 0 0 => 1
false true false => 0 1 0 => 2
false false false => 0 0 0 => 0
true true true => 1 1 1 => 5
```

And when you instantiate a new dog, you just give it the values, like

```rb
class Puppy < ApplicationRecord
  include Bitfields
  bitfield :puppy_bits, 1 => :has_chew_toy, 2 => :good_walker, 4 => :likes_pets
end

puppy = Puppy.new(has_chew_toy: true, good_walker: true)
puppy.likes_toys # true
puppy.puppy_bits # 3
```

This is pretty cool use of binary logic! And under the surface it's using [bitwise operators](https://github.com/grosser/bitfields/blob/master/lib/bitfields.rb#L171) to create the relationships.

## Final Note

I really love learning about bitwise operators because it takes something that seems really scary and illuminates it. Bitwise operators are just like the operators we learn in elementary school, but for a numeric system we aren't familiar with. While I love this implementations, for people less familiar with the operators, the syntax can be really confusing because it looks like Boolean logic but is really different. For that reason, I really like solutions that have comments and are well documented, at least recognizing the use of a bitwise operator in a codebase.

I learned a lot writing this post! If you'd like to explore these operators more in depth I've left some resources below.

## Resources

Here's a collection of some cool stuff I read in forming this blog post and some code:

* [Mozilla's wiki on Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)
* [Bitwise Operators in Ruby](https://www.calleerlandsson.com/rubys-bitwise-operators/)
* [my javascript tic-tac-toe](https://github.com/loganmeetsworld/js-tic-tac-toe/tree/lm/master)
* [really random helpful passage on tic-tac-toe in "Using Macromedia Flash MX" by Michael Hurwicz, Laura McCabe](https://books.google.com/books?id=zsti09XFNbEC&pg=PA246&lpg=PA246&dq=tic+tac+toe+bitwise+operators&source=bl&ots=u5VzY_PCUx&sig=ekn1-fpmR33CnNSDD2z0xnRASOQ&hl=en&sa=X&ved=0ahUKEwjM1--yqvPWAhXH2SYKHZQ4C2QQ6AEIUjAH#v=onepage&q=tic%20tac%20toe%20bitwise%20operators&f=true)
* [`secure_compare` docs](https://api.rubyonrails.org/v5.1/classes/ActiveSupport/SecurityUtils.html)
* [Timing Attacks against String Comparison by Nick Malcolm](https://thisdata.com/blog/timing-attacks-against-string-comparison/)
* [`bitfields` rails gem](https://github.com/grosser/bitfields)

