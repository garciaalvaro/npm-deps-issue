This project showcases a possible bug in *npm v7*.

The problem is that *npm v7* does not install linked local packages dependencies.
To see the behaviour of *npm v6* vs *v7*, this repository has 2 branches: `package-lock-v1` and `package-lock-v2`.

---

To reproduce:

- With *node-14* and *npm-6* installed, checkout branch `package-lock-v1`, go to `./app` and run `npm install`. The produced `node_modules` folder structure is:

```
node_modules
	.bin
	my-local-pkg
		node_modules
			typescript
	prettier
```

- With *node-15* and *npm-7* installed, checkout branch `package-lock-v2`, go to `./app` and run `npm install`. The produced `node_modules` folder structure is:

```
node_modules
	.bin
	my-local-pkg
	prettier
```

Compare the two outputs, *npm v7* does not install `my-local-pkg` dependencies, there is no `node_modules` folder generated in the linked `../my-local-pkg`.
