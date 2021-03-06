# Deep Lizard's Course on [DL Fundamentals](https://deeplizard.com/learn/playlist/PLZbbT5o_s2xq7LwI2y8_QtvuXZedL6tQU) and [tf.Keras](https://deeplizard.com/learn/playlist/PLZbbT5o_s2xrwRnXk_yCPtnqqo4_u2YGL)
__Previously, we could access the Dense module from Keras with the following import statement__
> <font color="purple">from</font> keras<font color="purple">.</font>layers <font color="purple">import</font> <font color="orange">Dense</font>

__Now, using Keras with TensorFlow, the import statement looks like this:__
> <font color="purple">from</font> tensorflow<font color="purple">.</font>keras<font color="purple">.</font>layers <font color="purple">import</font> <font color="orange">Dense</font>
___
## Major Changes
__Before TensorFlow Integration__ <br>
<font color="purple">import</font> <font color="orange">keras</font><br>
<font color="purple">from</font> keras<font color="purple">.</font>models <font color="purple">import</font> <font color="orange">Sequential</font><br>
<font color="purple">from</font> keras<font color="purple">.</font>layers <font color="purple">import</font> <font color="orange">Activation</font><br>
<font color="purple">from</font> keras<font color="purple">.</font>layers<font color="purple">.</font>core <font color="purple">import</font> <font color="orange">Dense</font><br>
<font color="purple">from</font> keras.layers.normalization <font color="purple">import</font> <font color="orange">BatchNormalization</font><br>
<font color="purple">from</font> keras.layers.convolutional <font color="purple">import</font> <font color="orange">Conv2D</font><br>
<font color="purple">from</font> keras<font color="purple">.</font>optimizers <font color="purple">import</font> <font color="orange">Adam</font><br>
<font color="purple">from</font> keras<font color="purple">.</font>metrics <font color="purple">import</font> <font color="orange">categorical_crossentropy</font><br>
<font color="purple">from</font> keras.preprocessing.image <font color="purple">import</font> <font color="orange">ImageDataGenerator</font><br>


__After TensorFlow Integration__ <br>
<font color="purple">import</font> <font color="orange">tensorflow</font><br>
<font color="purple">from</font> tensorflow <font color="purple">import</font> <font color="orange">keras</font><br>
<font color="purple">from</font> tensorflow<font color="purple">.</font>keras<font color="purple">.</font>models <font color="purple">import</font> <font color="orange">Sequential</font><br>
<font color="purple">from</font> tensorflow<font color="purple">.</font>keras.layers <font color="purple">import</font> <font color="orange">Activation, Dense, BatchNormalization, Conv2D</font><br>
<font color="purple">from</font> tensorflow<font color="purple">.</font>keras<font color="purple">.</font>optimizers <font color="purple">import</font> <font color="orange">Adam</font><br>
<font color="purple">from</font> tensorflow.<font color="purple"></font>keras<font color="purple">.</font>metrics <font color="purple">import</font> <font color="orange">categorical_crossentropy</font><br>
<font color="purple">from</font> tensorflow<font color="purple">.</font>keras<font color="purple">.</font>preprocessing<font color="purple">.</font>image <font color="purple">import</font> <font color="orange">ImageDataGenerator</font><br>
___




```diff
+ text in green
- text in red
# text in gray
! text in orange
@@ text in purple (and bold)@@
```
