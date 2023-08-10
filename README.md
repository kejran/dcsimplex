# dcsimplex

A C++ port of [OpenSimplex2-based noise generator by KdotJPG](https://github.com/KdotJPG/Cave-Tech-Demo).

It features: 
* Generation of gradient derivatives
* Optimization for iterative sampling along an axis
* Fixed three-dimensional input.

It was used for cave generation in my [3DS block game](https://github.com/kejran/ctraft).

## Usage 
```cpp
dcs::Seed seed(0);
dcs::Generator generator(seed);
generator.reset(0, 0);
for (int i = 0; i < 10; ++i)
    float f = generator.sample(x * 0.1f);
```
or, with derivatives:
```cpp
dcs::Seed seed(0);
dcs::DrvGenerator generator(seed);
generator.reset(0, 0);
for (int i = 0; i < 10; ++i) {
    // value, x, y ,z
    std::array<float, 4> f; 
    generator.sampleDrv(f, x * 0.1f);
}
```
Keep in mind the seed contains a lookup table and thus needs to be kept alive along with the generator. 

The generator itself is almost free, so I would suggest to keep the seeds persistent, and treat generators as disposable instead.
