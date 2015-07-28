
# Benchmarking

The approach presented here is rather simple, I didn't want to spend too much time setting testing environment, and came with a simplest solution.

We put three different builds in their own dist directory, and so:

* `dist_base` for _base_ build,
* `dist_enhanced` for _optimized_ build,
* `dist_enh_nojq` for _OptimizedJquery_ build

More info about these builds you'll find in [optimization.md](optimization.md).

## `!test.html`

Main file for testing is `_benchs/index.html`. It contains HTML fixtures. There are two fixtures:

* div#sampleContent for _small content_
* div#largeContent for _large content_

To read more about them go to "Test Files" section in [optimization.md](optimization.md).

### Scenario

You can simply understand them as a TC. All it does is to expose `window.setTest` function that will setup proper logic for test iteration method.

### Changing Build/Scenario

Both builds and test scenario are "selected" simply by uncommenting a proper line. Open `_benchs/index.html` file and uncomment proper script. **WARNING** this fille is pretty big, so make sure that you use an editor that won't freeze during syntax highlighting.

#### Change Build

You change the build by uncommenting one of following three script tags.

```html
<!-- Uncomment single line of any below, to include a proper build -->
<!-- <script src="../lib/jquery/jquery.js"></script><script src="../dist_base/quail.jquery.js"></script><script>window.jsonPath = '../dist_base';</script> -->
<!-- <script src="../lib/jquery/jquery.js"></script><script src="../dist_enhanced/quail.jquery.js"></script><script>window.jsonPath = '../dist_enhanced';</script> -->
<script src="../dist_enh_nojq/jquery.js"></script><script src="../dist_enh_nojq/quail.jquery.js"></script><script>window.jsonPath = '../dist_enh_nojq';</script>
```

You need to look at dist directory to know which version is this. These are respectively:

* `dist_base`
* `dist_enhanced`
* `dist_enh_nojq`

#### Change Scenario

```html
<!-- Uncomment single line of any below, to run proper scenario -->
<script src="scenarios/quail.smallContent.js"></script>
<!-- <script src="scenarios/quail.largeContent.js"></script> -->
<!-- <script src="scenarios/quail.smallContent.wcag2.js"></script> -->
<!-- <script src="scenarios/quail.largeContent.wcag2.js"></script> -->
<!-- <script src="scenarios/selector.imgHasAlt.js"></script> -->
<!-- <script src="scenarios/selector.aAdjacentWithSameResourceShouldBeCombined.js"></script> -->
<!-- <script src="scenarios/selector.quailCss.js"></script> -->
<!-- <script src="scenarios/selector.quailCssSingle.js"></script> -->
```

It's similar to the build selection. You simply need to uncomment one script.

#### How Do I?

* **Change iterations count?**

	You need to modify first parameter of `tester.start()` method in `index.html`.
	
* **Set scope for selector.x scenario?**

	You need to modify second parameter of `window.setTest()` method in `index.html`. E.g. setting it to `window.setTest( tester, '#sampleContent' );` will make it to look inside _small content_. 