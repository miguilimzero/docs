# Animations
## Changing details of animated images

[TOC]

## Detect animations

### Check the current image instance for animation

> public Image::isAnimated(): bool

Returns `true` if the image is animated. Otherwise `false` is returned.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// true
$result = $manager->read('images/animation.gif')->isAnimated();
```

## Editing animations

### Changing the animation frames

> public Image::sliceAnimation(int $offset, null|int $length = null): ImageInterface

Extract animation frames based on given values and discard the rest. The offset
parameter can be used to set the starting point of the new animation; all
frames before the offset are discarded. The length parameter is optional. It
specifies how many frames to read after the offset. By default, all frames up
to the end of the animation are read.

#### Parameters

| Name | Type | Description |
| - | - | - |
| offset | integer | Starting point of the new animation |
| length | null or integer | Frames to read after the offset (optional) |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// discard the first 20 frames and read the following 10 frames as new animation
$image = $image->sliceAnimation(20, 10);
```

### Reading the Animation Iteration Count

> public Image::loops(): int

Read the count of iterations of the animated image. `0` means the image loops continuously.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// return animation iteration count
$count = $image->loops();
```

### Changing the Animation Iteration Count

> public Image::setLoops(int $count): ImageInterface

Change the number of iterations the animation should loop over. Set to `0` to loop continuously.

#### Parameters

| Name | Type | Description |
| - | - | - |
| count | integer | Number of animation iterations |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// animation should only run once
$image = $image->setLoops(1);
```

### Removing animation

> public Image::removeAnimation(int|string $position = 0): ImageInterface

Discards all animation frames of the current image instance except the one at
the given position. Turns an animated image into a static one.

It is possible to specify the position as integer and string values. With the
former, the exact position passed is searched for, while string values must
represent a percentage value between `0%` and `100%` and the respective frame
position is only determined approximately.

If an integer is specified, the method throws an exception if the respective
position is not found. This does not happen with percentage values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer or string | Position of the frame that will be left. |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// Turn the animation into a static image displaying the frame at position 5
$image = $image->removeAnimation(5);

// do the same by choosing animation frame at 25% of the whole animation
$image = $image->removeAnimation('25%');

```
