# `import equinox.internal as eqxi`

This namespace is 'semi-public', and contains advanced, undocumented, features. It is primarily for functionality used by privileged downstream libraries, like [Diffrax](https://github.com/patrick-kidger/diffrax). You can find the full list of available features in `__init__.py`.

This means that it is full of lots of fun toys for the JAX enthusiast! If you're reading this, then it may be because I've pointed you at some of the functionality in this directory, as the appropriate tool to solve your problem. Enjoy! :)

A few of the highlights available here are:

**loop/** A while loop which may be backpropagated through, using an online checkpointing scheme. Also implements a recursive checkpointed ("treeverse") scan.

**errors.py:** Runtime errors. For verifying arguments or for checking that a computation succeeded. Only tested on CPU.

**noinline.py:** MLIR sub-graphs. Can reduce compile times by removing the inlining of a function called repeatedly. Also makes it possible to iteratively recompile: change and recompile just the sub/super-computation, without needing to recompile the whole computation graph. Only tested on CPU.

**omega.py**: Neat syntax for tree-mapping arithmetic. E.g. `(x**ω + y**ω).ω == jtu.tree_map(operator.add, x, y)`. See also [tree-math](https://github.com/google/tree-math), for a similar idea but without the neat syntax.

**primitive.py:** Provides a filter-like syntax for defining new primitives, whose rules accept PyTrees of arbitrary objects. Also provides a helper for automatically defining batch rules such that `transform(vmap(prim))` is lowered to `vmap(transform(prim))`. (Useful for higher-order primitives.)

---

Nothing here comes with any stability guarantees. APIs may changed or be removed at any time.
