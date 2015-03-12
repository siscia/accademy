---
title: Clojure Presentation
layout: post
---

# Clojure Presentation Track

## Intro

Hello Everybody,

my name is Simone Mosciatti, I am Italian and I am going to introduce Clojure and functional programming.

I do have a weird accent, so if you cannot understand what I am saying please just raise your hand.

Let me ask you first:

*Who know clojure ?* few hands expected
*Who know functional programming ?* slightly more hands

Thank you.

## Clojure intro

Clojure is a Lisp dialect that run on the JVM.

Is definitely more than fast enough for most application but it is extremely slow in startup time.

Clojure is a very productive language and it is used for a lot of data intensive application and to run web application.

Actually is a good fit for most task, I won't write a micro controller in clojure though.

## What clojure looks like ?

``` clojure
(def one-to-ten (range 1 (inc 10))) ;; a variable

(defn multiply-by-two [num] ;; a function
  (* num 2))

(map multiply-by-two (range 1 (inc 10))) ;; an expression
;; (2 4 6 8 10 12 14 16 18 20) this is a comment
```

Ok, it is different from what you usually see but it is an extremely simple concept.

The first thing after the bracket is a function, all the other things are arguments for such function, of course, argument to a function can be other function call.

That it's.

## Some simple example

### Simple Math

Let's try to make some math...

``` clojure
(+ 41 1)
;; 42
(* 21 2)
;; 42
(- 2015 1994)
;; 21
(/ 4 2)
;; 2
(/ 4 3)
;; 4/3 Woooaaaah
(* (/ 4 3) (/ 5 3))
;; 20/9
(float 20/9)
;; 2.2222223
(Math/sqrt 16) ;; Please attention here
;; 4.0
```

Ok the math works.

If you have paid attention you are wondering about the square root...

`Math/sqrt` actually is java call, clojure is completely interopatible with the host platform, that usually is Java.

This means that you can use any Java library and actually is pretty common. (Usually it is a good idea to write a thin layer to wrap the Java library but it is not required.)

### Datatype

We have pretty much any datatype you would expect.

#### Fundamental

``` clojure
(def string "normal string")
(def number 42) ;; and float and rations
(def keyword :key) ;; please ask, it is just a type of string
```

#### Sequential

Sequential stuff such list and vector.

``` clojure
(def primes-vector [1 2 3 5 7 11]) ;; extremely fast
(def string-list '("a" "b" "c")) ;; why the hypes ???
```

Those sequential element can contains anything.

#### Tables and Sets

This is an hash table, are extremely fast, easy to manipulate and are a good fit for a lot of problems.

``` clojure
(def my-self
    {:name "Simone Mosciatti"
     :age 20
     :work "unemployed"
     :girlfriend "Extremely far from HERE :-("})
```

Simple sets

``` clojure
(clojure.set/union #{1 2 3} #{3 4 5}) ;; ??? namespace
;; #{1 4 3 2 5}
```
Also those are extremelly fast.

### Control flow

There are a lot of way to control the logical flow in clojure, let me show the simplest.

``` clojure
(if (= (+ 41 1) (* 21 2))
	:ok
	:ahhh-the-is-ending)
;; :ok phewwww....
(case (first "abc")
	\b "This is a b"
	\a "We got an a"
	"Something else")
"Something else"
```

## Function

### Simple function

``` clojure
(defn name-of-the-function
	"The documentation of the function"
	[the-argument other-argument]
	(+ the-argument other-argument))
#'user/name-of-the-function
user> (name-of-the-function 3 4)
7
```

Of course the same function will be written as

``` clojure
user> (defn sum-two-number [a b]
	(+ a b))
#'user/sum-two-number
```

Clojure provide support for anonymous function

``` clojure
user> ( (fn [a] (+ 1 a)) 3)
4
user> ( #(+ 1 % ) 3) ;; shortcut
4
```

Function are first order citizen, so they can be passed around like number, and can be returned by other function...

``` clojure
(defn add-n [n] (fn [a] (+ a n)))
#'user/add-n
user> (defn add-five [a]
	(let [add-four (add-n 4)]
	  (add-four (+ a 1))))
#'user/add-five
user> (add-five 5)
10
user> (defn transform-number [function n]
	     (function n))
#'user/transform-number
user> (transform-number add-five 4)
9
user> (transform-number (add-n 6) 4)
10
user> (transform-number add-n 4)
#<user$add_n$fn__2929 user$add_n$fn__2929@1c69143c>
user> ( (transform-number add-n 4) 4)
8
```

## Immutability and variable

So, we have played around with clojure but I have never modified a variable, this because I cannot. (It is not exactly true but lets keep stuff simple...)

### How can we make any useful thing without modify variable ?

In clojure, similarly to other functional languages, you usually create a funnel/chain of transformations, you plug your input in, and you get your output out.

This "funnel/chain of transformations" is the composition of several functions.

In idiomatic clojure any function is a pure function, given the same input you will get the same output, any single time, and the function do not modify the environment.

This is extremely powerful:

``` clojure
(def my-self
    {:name "Simone Mosciatti"
     :age 20
     :work "unemployed"
     :girlfriend "Extremely far from HERE :-("})

(defn split-name [{:keys [name] :as person}]
	(let [[name surname] (clojure.string/split name #" ")]
	  (assoc person :firstname name :lastname surname)))

(defn birthday [{:keys [age] :as person}]
	(assoc person :age (inc age)))

(defn find-job [person]
	(assoc person :work "Amazing company"))

(defn meet-girlfriend [person]
	(assoc person :girlfriend "Just next to me :-)"))

(defn perfect [user]
	(birthday (find-job (meet-girlfriend (split-name user)))))
(defn more-idiomatic-perfect [person]
	(-> person split-name birthday find-job meet-girlfriend))
(def perfect-perfect (comp split-name birthday find-job meet-girlfriend))
```

How it this approach useful ?

Any function can be tested in isolation, test is extremely simple, and atomic.

This approach scale, even with thousand of LOC we are still using pure function that are trivial to test.

Small recap: Clojure do not modify variable, it modify, and combine function in such a way to create a funnel/chain, where you plug in your input value and where you get out your output value.

Function in idiomatic clojure are simple, small, and pure, are extremely easy to test (maybe even too easy) and to reason about.

## End

We have barely scratch the surface, but hopefully I got you interested in Clojuer.

Thanks for listening, and if you have any question just let know :)
