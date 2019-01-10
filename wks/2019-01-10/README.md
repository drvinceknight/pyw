# 2019-01-10

Goals for the session:

- Meet;
- Invite to slack room;
- Discuss purpose of this group;
- Discuss what Python is and why it is particular;
- Discuss resources;
- Go over some minor python tools.

## Meet

Introductions + uses of Python.

> My name is Vince and I have been using Python for more than 6 years having
> been a mathematica user and wanting something "free". I
> regularly review Python code, teach Python and also use it in game theoretic
> and stochastic mathematics.

## Purpose of the group

Initial proposal:

- 1 hour: some directed content.
- 1 hour: open space for programming.

## Why is Python particular

- Writer and reader friendly.
- Production ready.
- Open source.
- Community.

## Resources

- Local groups:

    - [PyData Cardiff](https://www.meetup.com/PyData-Cardiff-Meetup/)
    - [PyDiff](https://www.meetup.com/pydiff/)
    - Our slack channel.

- Podcasts:

    - [https://talkpython.fm/](https://talkpython.fm/)
    - [https://www.podcastinit.com/](https://www.podcastinit.com/)
    - [https://pythonbytes.fm/](https://pythonbytes.fm/)

- Twitter accounts:

    - [https://twitter.com/NumFocus](https://twitter.com/NumFocus)
    - [https://twitter.com/gvanrossum](https://twitter.com/gvanrossum)
    - [https://twitter.com/jakevdp](https://twitter.com/jakevdp)
    - ...

- Books:

    - [Fluent Python](https://www.amazon.co.uk/Fluent-Python-Luciano-Ramalho/dp/1491946008/ref=sr_1_1?ie=UTF8&qid=1546882783&sr=8-1&keywords=fluent+python)
    - [Python tricks](https://smile.amazon.co.uk/Python-Tricks-Buffet-Awesome-Features/dp/1775093301/ref=sr_1_1?ie=UTF8&qid=1546882821&sr=8-1&keywords=python+tricks)
    - [Elegant Scipy](https://smile.amazon.co.uk/Elegant-SciPy-Juan-Nunez-iglesias/dp/1491922877/ref=sr_1_sc_1?ie=UTF8&qid=1546885482&sr=8-1-spell&keywords=elevant+scipy)
    - [Effective Computation in Physics](https://smile.amazon.co.uk/Effective-Computation-Physics-Anthony-Scopatz/dp/1491901535/ref=sr_1_fkmr2_1?ie=UTF8&qid=1547118583&sr=8-1-fkmr2&keywords=efficient+computation+in+physics)
    - [Clean code](https://www.amazon.co.uk/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882/ref=sr_1_1?ie=UTF8&qid=1546882756&sr=8-1&keywords=clean+code)


## Some Python

#### Jupyter versus scripts

- What is the difference?
- Why/when should I use either?
- This is an often spoken about topic:

  - https://conferences.oreilly.com/jupyter/jup-ny/public/schedule/detail/68282
  - https://docs.google.com/presentation/d/1XmbeH_sdOKqhi05_FbH2EdRw948i8IvBz1PdfJGbhf4/edit#slide=id.g46d7a36656_0_31

#### Tools for Modularisation

- `def` and `assert`

  ```
  import math

  a = 0
  b = 3.14
  mid = (a + b) / 2
  while math.cos(mid) > 10 ** -2:
      if math.cos(a) * math.cos(mid) > 0:
          a, mid = mid, (mib + b) / 2
      else:
          b, mid = mid, (mib + a) / 2
  mid, math.cos(mid)
  ```

  to:

  ```python
  import math
  import numpy as np

  def compute_mid_point(*points):
      """
      Computes the "mid point" of any given number of points.
      """
      return np.mean(points)

  assert compute_mid_point(2, 3) == 2.5
  assert compute_mid_point(5, 4) == 4.5
  assert compute_mid_point(1, 1, 1) == 1

  def same_signed_value(function, *points):
      """
      Checks if function(points) have the same sign
      """
      return min(points) * max(points) > 0

  assert same_signed_value(math.cos, 2, 3) is True
  assert same_signed_value(math.cos, 0, math.pi) is False

  def bisection(function, left_boundary, right_boundary, tol=10 ** -2):
      """
      Using bisection to obtain a root of `function`
      """
      assert not same_signed_value(function, left_boundary, right_boundary), "Boundary points must have different function value"
      mid = compute_mid_point(left_boundary, right_boundary)
      while function(mid) > tol:
          if same_signed_value(function, left_boundary, mid):
              left_boundary, mid = mid, compute_mid_point(mid, right_boundary)
          else:
              right_boundary, mid = mid, compute_mid_point(left_boundary, mid)
      return mid

  assert math.cos(bisection(math.cos, left_boundary=0, right_boundary=math.pi)) < 10 ** -2
  assert math.sin(bisection(math.sin, left_boundary=0, right_boundary=math.pi)) < 10 ** -2
  ```

- `import`
- `if __name__ == "__main__":`
- `dir`
- [`black`](https://black.readthedocs.io/en/stable/)

#### Some python "tricks"

- `enumerate`
- `zip`
- Arrays in python

#### Don't write code
