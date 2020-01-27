# UX3D_lights_imageBased

## Contributors

* Gary Hsu, Microsoft
* Mike Bond, Adobe
* Norbert Nopper, UX3D
* Alexey Knyazev
* Benjamin Schmithüsen, UX3D
* Fabian Wahlster, UX3D
* `Please add or remove!`

## Status

Draft

## Dependencies

Written against the glTF 2.0 spec.

## Overview

This extension provides the ability to define image-based lights in a glTF scene. Image-based lights consist of an environment map that represents specular radiance for the scene as well as irradiance information.

Many 3D tools and engines support image-based global illumination but the exact technique and data formats employed vary. Using this extension, tools can export and engines can import image-based lights and the result should be highly consistent.

This extension specifies exactly one way to format and reference the environment map to be used. The goals of this are two-fold. First, it makes implementing support for this extension easier. Secondly, it ensures that rendering of the image-based lighting is consistent across runtimes.

A conforming implementation of this extension must be able to load the image-based environment data and render the PBR materials using this lighting.

## Defining an Image-Based Light

The `UX3D_lights_imageBased` extension defines a array of image-based lights at the root of the glTF and then each scene can reference one. Each image-based light definition consists of a single cubemap that describes the specular radiance of the scene including a lookup table texture, the l=2 spherical harmonics coefficients or another cubemap for diffuse irradiance, and also rotation, brighness factor, and offset values.

An example using SH for diffuse irradiance:

```json
"extensions": {
    "UX3D_lights_imageBased" : {
        "imageBasedLights": [
            {
                "rotation": [0, 0, 0, 1],
                "brightnessFactor": 1.0,
                "brightnessOffset": 0.0,
                "specularEnvironmentTexture": 0,
                "specularLookupTexture": 1,
                "diffuseSphericalHarmonics": [
                    [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0],
                    [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0],
                    [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
                ]
            }
        ]
    }
}
```

An example using a cubemap for diffuse irradiance:

```json
"extensions": {
    "UX3D_lights_imageBased" : {
        "imageBasedLights": [
            {
                "rotation": [0, 0, 0, 1],
                "brightnessFactor": 1.0,
                "brightnessOffset": 0.0,
                "specularEnvironmentTexture": 0,
                "specularLookupTexture": 1,
                "diffuseEnvironmentTexture": 2
            }
        ]
    }
}
```

## Specular BRDF integration and Irradiance Coefficients

This extension uses a prefiltered environment map to define the specular lighting utilizing the split sum approximation. More information:
- [Specular BRDF integration in Google Filament](https://google.github.io/filament/Filament.md.html#lighting/imagebasedlights/processinglightprobes)
- [Pre-Filtered Environment Map in Unreal Engine 4](https://blog.selfshadow.com/publications/s2013-shading-course/karis/s2013_pbs_epic_notes_v2.pdf)

This extension can use spherical harmonic coefficients to define irradiance used for diffuse lighting. Coefficients are calculated for the first 3 SH bands (l=2) and take the form of a 9x3 array. More information:
- [Realtime Image Based Lighting using Spherical Harmonics](https://metashapes.com/blog/realtime-image-based-lighting-using-spherical-harmonics/)
- [An Efficient Representation for Irradiance Environment Maps](http://graphics.stanford.edu/papers/envmap/)

## Adding Light Instances to Scenes

Each scene can have a single IBL light attached to it by defining the `extensions` and `UX3D_lights_imageBased` property and, within that, an index into the `imageBasedLights` array using the `imageBasedLight` property.

```json
"scenes" : [
    {
        "extensions" : {
            "UX3D_lights_imageBased" : {
                "imageBasedLight" : 0
            }
        }
    }
]
```

## Shader Code Implementation

```
finalSampledColor = sampledColor * brightnessFactor + brightnessOffset;
```

## Image Encoding

### Texture Restrictions

- `specularEnvironmentTexture` and `diffuseEnvironmentTexture` (when used) must refer to a texture referring to a KTX2 image of **Cubemap** type as defined in KTX2, Section 4.3. Namely:
  - `pixelHeight` must be greater than 0.
  - `pixelDepth` must be 0.
  - `layerCount` must be 0.
  - `faceCount` must be 6.
- The image must contain mip levels.
- The transfer function for all image formats must be linear.
- Cubemaps orientation must be aligned with [glTF coordinate system](../../../../specification/2.0#coordinate-system-and-units).

### Normal Quality

Data must be stored as a KTX2 image.

## Example

```json
{
    "asset": { "version": "2.0" },
    "extensionsUsed": [ "UX3D_lights_imageBased" ],
    "extensionsRequired": [ "UX3D_lights_imageBased" ],
    "scenes": [
        {
            "extensions": {
                "UX3D_lights_imageBased" : {
                    "imageBasedLight": 0
                }
            }
        }
    ],
    "extensions": {
        "UX3D_lights_imageBased" : {
            "imageBasedLights": [
                {
                    "name": "GGX",
                    "specularEnvironmentTexture": 0,
                    "diffuseEnvironmentTexture": 1,
                    "specularLookupTexture": 2
                }
            ]
        }
    },
    "textures": [
        {
            "name": "Specular Environment Texture",
            "source": 0,
        },
        {
            "name": "Diffuse Environment Texture",
            "source": 1
        },
        {
            "name": "Specular LUT Texture",
            "source": 2
        }
    ],
    "images": [
        { "uri": "environmentSpecular.ktx2" },
        { "uri": "environmentDiffuse.ktx2" },
        { "uri": "brdfLUT.png" }
    ]
}
```

## glTF Schema Updates

* **JSON schema**:
- [glTF.UX3D_lights_imageBased.schema.json](schema/glTF.UX3D_lights_imageBased.schema.json)
- [imageBasedLight.schema.json](schema/imageBasedLight.schema.json)
- [scene.UX3D_lights_imageBased.schema.json](schema/scene.UX3D_lights_imageBased.schema.json)

## Known Implementations

[glTF-Sample-Viewer](https://github.com/KhronosGroup/glTF-Sample-Viewer/tree/pbr-next)
