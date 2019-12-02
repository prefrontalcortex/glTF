# Properties Reference

## Objects
* [accessor](#accessor)
   * [sparse](#sparse)
      * [indices](#indices)
      * [values](#values)
* [animation](#animation)
   * [animation sampler](#animation-sampler)
   * [channel](#channel)
      * [target](#target)
* [asset](#asset)
* [buffer](#buffer)
* [bufferView](#bufferview)
* [camera](#camera)
   * [orthographic](#orthographic)
   * [perspective](#perspective)
* [extension](#extension)
* [extras](#extras)
* [glTF](#gltf) (root object)
* [image](#image)
* [material](#material)
   * [pbrMetallicRoughness](#pbrmetallicroughness)
* [mesh](#mesh)
   * [primitive](#primitive)
* [node](#node)
* [sampler](#sampler)
* [scene](#scene)
* [skin](#skin)
* [texture](#texture)
* [textureInfo](#textureinfo)
* [Appendix A: Tangent Space Recalculation](#appendix-a-tangent-space-recalculation)
* [Appendix B: BRDF Implementation](#appendix-b-brdf-implementation)
* [Appendix C: Spline Interpolation](#appendix-c-spline-interpolation)

## Extensions

* [ktx2](#ktx2)
* [light](#light)
   * [Light Shared](#Light-Shared)
   * [spot](#spot)
   * [image based Light](#image-Based-Light)
* [materials](#materials)
   * [clearcoat](#clearcoat)
   * [pbrSpecularGlossiness](#pbrSpecularGlossiness)
   * [specular](#specular)
   * [unlit](#unlit)
* [textures](#textures)
   * [basisu](#Texture-basisu)
   * [astc hdr](#Texture-astc-hdr)
   * [bc6h](#Texture-bc6h)
   * [transform](#Texture-Transform)





---------------------------------------
<a name="reference-accessor"></a>
# Accessor

A typed view into a bufferView.  A bufferView contains raw binary data.  An accessor provides a typed view into a bufferView or a subset of a bufferView similar to how WebGL's `vertexAttribPointer()` defines an attribute in a buffer.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**bufferView**|`integer`|The index of the bufferView.|No|
|**byteOffset**|`integer`|The offset relative to the start of the bufferView in bytes.|No, default: `0`|
|**componentType**|`integer`|The datatype of components in the attribute.| :white_check_mark: Yes|
|**normalized**|`boolean`|Specifies whether integer data values should be normalized.|No, default: `false`|
|**count**|`integer`|The number of attributes referenced by this accessor.| :white_check_mark: Yes|
|**type**|`string`|Specifies if the attribute is a scalar, vector, or matrix.| :white_check_mark: Yes|
|**max**|`number` `[1-16]`|Maximum value of each component in this attribute.|No|
|**min**|`number` `[1-16]`|Minimum value of each component in this attribute.|No|
|**sparse**|`object`|Sparse storage of attributes that deviate from their initialization value.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-animation"></a>
# Animation

A keyframe animation.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**channels**|channel `[1-*]`|An array of channels, each of which targets an animation's sampler at a node's property. Different channels of the same animation can't have equal targets.| :white_check_mark: Yes|
|**samplers**|animation sampler `[1-*]`|An array of samplers that combines input and output accessors with an interpolation algorithm to define a keyframe graph (but not its target).| :white_check_mark: Yes|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-animation-sampler"></a>
# Animation sampler

Combines input and output accessors with an interpolation algorithm to define a keyframe graph (but not its target).

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**input**|`integer`|The index of an accessor containing keyframe input values, e.g., time.| :white_check_mark: Yes|
|**interpolation**|`string`|Interpolation algorithm.|No, default: `"LINEAR"`|
|**output**|`integer`|The index of an accessor, containing keyframe output values.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.






---------------------------------------
---------------------------------------
<a name="reference-asset"></a>
# Asset

Metadata about the glTF asset. Not implemented in codebase.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**copyright**|`string`|A copyright message suitable for display to credit the content creator.|No|
|**generator**|`string`|Tool that generated this glTF model.  Useful for debugging.|No|
|**version**|`string`|The glTF version that this asset targets.| :white_check_mark: Yes|
|**minVersion**|`string`|The minimum glTF version that this asset targets.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.






---------------------------------------
---------------------------------------
<a name="reference-buffer"></a>
# Buffer

A buffer points to binary geometry, animation, or skins.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**uri**|`string`|The uri of the buffer.|No, default `""`|
|**byteLength**|`integer`|The total byte length of the buffer view.| :white_check_mark: Yes|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.






---------------------------------------
---------------------------------------
<a name="reference-bufferview"></a>
# BufferView

A view into a buffer generally representing a subset of the buffer.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**buffer**|`integer`|The index of the buffer.| :white_check_mark: Yes|
|**byteOffset**|`integer`|The offset into the buffer in bytes.|No, default: `0`|
|**byteLength**|`integer`|The length of the bufferView in bytes.| :white_check_mark: Yes|
|**byteStride**|`integer`|The stride, in bytes.|No|
|**target**|`integer`|The target that the GPU buffer should be bound to.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-camera"></a>
# Camera

A camera's projection.  A node can reference a camera to apply a transform to place the camera in the scene.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**orthographic**|`object`|An orthographic camera containing properties to create an orthographic projection matrix.|No|
|**perspective**|`object`|A perspective camera containing properties to create a perspective projection matrix.|No|
|**type**|`string`|Specifies if the camera uses a perspective or orthographic projection.| :white_check_mark: Yes|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-channel"></a>
# Channel

Targets an animation's sampler at a node's property. Not implemented in codebase.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**sampler**|`integer`|The index of a sampler in this animation used to compute the value for the target.| :white_check_mark: Yes|
|**target**|`object`|The index of the node and TRS property to target.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-extension"></a>
# Extension

Dictionary object with extension-specific objects.

Additional properties are allowed.

* **JSON schema**: [extension.schema.json](schema/extension.schema.json)





---------------------------------------
---------------------------------------
<a name="reference-extras"></a>
# Extras

Application-specific data.

> **Implementation Note:** Although extras may have any type, it is common for applications to
store and access custom data as key/value pairs. As best practice, extras should be an Object
rather than a primitive value for best portability.





---------------------------------------
---------------------------------------
<a name="reference-gltf"></a>
# GlTF

The root object for a glTF asset.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**extensionsUsed**|`string` `[1-*]`|Names of glTF extensions used somewhere in this asset.|No|
|**extensionsRequired**|`string` `[1-*]`|Names of glTF extensions required to properly load this asset.|No|
|**accessors**|accessor `[1-*]`|An array of accessors.|No|
|**animations**|animation `[1-*]`|An array of keyframe animations.|No|
|**asset**|`object`|Metadata about the glTF asset.|Yes|
|**buffers**|buffer `[1-*]`|An array of buffers.|No|
|**bufferViews**|bufferView `[1-*]`|An array of bufferViews.|No|
|**cameras**|camera `[1-*]`|An array of cameras.|No|
|**images**|image `[1-*]`|An array of images.|No|
|**materials**|material `[1-*]`|An array of materials.|No|
|**meshes**|mesh `[1-*]`|An array of meshes.|No|
|**nodes**|node `[1-*]`|An array of nodes.|No|
|**samplers**|sampler `[1-*]`|An array of samplers.|No|
|**scene**|`integer`|The index of the default scene.|No|
|**scenes**|scene `[1-*]`|An array of scenes.|No|
|**skins**|skin `[1-*]`|An array of skins.|No|
|**textures**|texture `[1-*]`|An array of textures.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.






---------------------------------------
---------------------------------------
<a name="reference-image"></a>
# Image

Image data used to create a texture. Image can be referenced by URI or [`bufferView`](#reference-bufferview) index. `mimeType` is required in the latter case.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**uri**|`string`|The uri of the image.|No, default `""`|
|**mimeType**|`string`|The image's MIME type.|No, default `""`|
|**bufferView**|`integer`|The index of the bufferView that contains the image. Use this instead of the image's uri property.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-indices"></a>
# Indices

Indices of those attributes that deviate from their initialization value.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**bufferView**|`integer`|The index of the bufferView with sparse indices. Referenced bufferView can't have ARRAY_BUFFER or ELEMENT_ARRAY_BUFFER target.| :white_check_mark: Yes|
|**byteOffset**|`integer`|The offset relative to the start of the bufferView in bytes. Must be aligned.|No, default: `0`|
|**componentType**|`integer`|The indices data type.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-material"></a>
# Material

The material appearance of a primitive.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|
|**pbrMetallicRoughness**|`object`|A set of parameter values that are used to define the metallic-roughness material model from Physically-Based Rendering (PBR) methodology. When not specified, all the default values of [`pbrMetallicRoughness`](#reference-pbrmetallicroughness) apply.|No|
|**normalTexture**|`object`|The normal map texture.|No|
|**occlusionTexture**|`object`|The occlusion map texture.|No|
|**emissiveTexture**|`object`|The emissive map texture.|No|
|**emissiveFactor**|`number` `[3]`|The emissive color of the material.|No, default: `[0,0,0]`|
|**alphaMode**|`string`|The alpha rendering mode of the material.|No, default: `"OPAQUE"`|
|**alphaCutoff**|`number`|The alpha cutoff value of the material.|No, default: `0.5`|
|**doubleSided**|`boolean`|Specifies whether the material is double sided.|No, default: `false`|

Additional properties are allowed.

## pbrMetallicRoughness


**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**baseColorFactor**|`number` `[4]`|The material's base color factor.|No, default: `[1,1,1,1]`|
|**baseColorTexture**|`object`|The base color texture.|No|
|**metallicFactor**|`number`|The metalness of the material.|No, default: `1`|
|**roughnessFactor**|`number`|The roughness of the material.|No, default: `1`|
|**metallicRoughnessTexture**|`object`|The metallic-roughness texture.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-mesh"></a>
# Mesh

A set of primitives to be rendered.  A node can contain one mesh.  A node's transform places the mesh in the scene.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**primitives**|primitive `[1-*]`|An array of primitives, each defining geometry to be rendered with a material.| :white_check_mark: Yes|
|**weights**|`number` `[1-*]`|Array of weights to be applied to the Morph Targets.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.






---------------------------------------
---------------------------------------
<a name="reference-node"></a>
# Node

A node in the node hierarchy.  When the node contains [`skin`](#reference-skin), all `mesh.primitives` must contain `JOINTS_0` and `WEIGHTS_0` attributes.  A node can have either a `matrix` or any combination of `translation`/`rotation`/`scale` (TRS) properties. TRS properties are converted to matrices and postmultiplied in the `T * R * S` order to compose the transformation matrix; first the scale is applied to the vertices, then the rotation, and then the translation. If none are provided, the transform is the identity. When a node is targeted for animation (referenced by an animation.channel.target), only TRS properties may be present; `matrix` will not be present.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**camera**|`integer`|The index of the camera referenced by this node.|No|
|**children**|`integer` `[1-*]`|The indices of this node's children.|No|
|**skin**|`integer`|The index of the skin referenced by this node.|No|
|**matrix**|`number` `[16]`|A floating-point 4x4 transformation matrix stored in column-major order.|No, default: `[1,0,0,0,0,1,0,0,0,0,1,0,0,0,0,1]`|
|**mesh**|`integer`|The index of the mesh in this node.|No|
|**rotation**|`number` `[4]`|The node's unit quaternion rotation in the order (x, y, z, w), where w is the scalar.|No, default: `[0,0,0,1]`|
|**scale**|`number` `[3]`|The node's non-uniform scale, given as the scaling factors along the x, y, and z axes.|No, default: `[1,1,1]`|
|**translation**|`number` `[3]`|The node's translation along the x, y, and z axes.|No, default: `[0,0,0]`|
|**weights**|`number` `[1-*]`|The weights of the instantiated Morph Target. Number of elements must match number of Morph Targets of used mesh.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-normaltextureinfo"></a>
# NormalTextureInfo

Reference to a texture.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**index**|`integer`|The index of the texture.| :white_check_mark: Yes|
|**texCoord**|`integer`|The set index of texture's TEXCOORD attribute used for texture coordinate mapping.|No, default: `0`|
|**scale**|`number`|The scalar multiplier applied to each normal vector of the normal texture.|No, default: `1`|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-occlusiontextureinfo"></a>
# OcclusionTextureInfo

Reference to a texture.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**index**|`integer`|The index of the texture.| :white_check_mark: Yes|
|**texCoord**|`integer`|The set index of texture's TEXCOORD attribute used for texture coordinate mapping.|No, default: `0`|
|**strength**|`number`|A scalar multiplier controlling the amount of occlusion applied.|No, default: `1`|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-orthographic"></a>
# Orthographic

An orthographic camera containing properties to create an orthographic projection matrix.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**xmag**|`number`|The floating-point horizontal magnification of the view.| :white_check_mark: Yes|
|**ymag**|`number`|The floating-point vertical magnification of the view.| :white_check_mark: Yes|
|**zfar**|`number`|The floating-point distance to the far clipping plane. `zfar` must be greater than `znear`.| :white_check_mark: Yes|
|**znear**|`number`|The floating-point distance to the near clipping plane.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-perspective"></a>
# Perspective

A perspective camera containing properties to create a perspective projection matrix.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**aspectRatio**|`number`|The floating-point aspect ratio of the field of view.|No|
|**yfov**|`number`|The floating-point vertical field of view in radians.| :white_check_mark: Yes|
|**zfar**|`number`|The floating-point distance to the far clipping plane.|No|
|**znear**|`number`|The floating-point distance to the near clipping plane.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.





---------------------------------------
---------------------------------------
<a name="reference-primitive"></a>
# Primitive

Geometry to be rendered with the given material.

**Related WebGL functions**: `drawElements()` and `drawArrays()`

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**attributes**|`object`|A dictionary object, where each key corresponds to mesh attribute semantic and each value is the index of the accessor containing attribute's data.| :white_check_mark: Yes|
|**indices**|`integer`|The index of the accessor that contains the indices.|No|
|**material**|`integer`|The index of the material to apply to this primitive when rendering.|No|
|**mode**|`integer`|The type of primitives to render.|No, default: `4`|
|**targets**|`object` `[1-*]`|An array of Morph Targets, each  Morph Target is a dictionary mapping attributes (only `POSITION`, `NORMAL`, and `TANGENT` supported) to their deviations in the Morph Target.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-sampler"></a>
# Sampler

Texture sampler properties for filtering and wrapping modes.

**Related WebGL functions**: `texParameterf()`

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**magFilter**|`integer`|Magnification filter.|No|
|**minFilter**|`integer`|Minification filter.|No|
|**wrapS**|`integer`|s wrapping mode.|No, default: `10497`|
|**wrapT**|`integer`|t wrapping mode.|No, default: `10497`|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-scene"></a>
# Scene

The root nodes of a scene.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**nodes**|`integer` `[1-*]`|The indices of each root node.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-skin"></a>
# Skin

Joints and matrices defining a skin.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**inverseBindMatrices**|`integer`|The index of the accessor containing the floating-point 4x4 inverse-bind matrices.  The default is that each matrix is a 4x4 identity matrix, which implies that inverse-bind matrices were pre-applied.|No|
|**skeleton**|`integer`|The index of the node used as a skeleton root.|No|
|**joints**|`integer` `[1-*]`|Indices of skeleton nodes, used as joints in this skin.| :white_check_mark: Yes|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.



---------------------------------------
---------------------------------------
<a name="reference-sparse"></a>
# Sparse

Sparse storage of attributes that deviate from their initialization value.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**count**|`integer`|Number of entries stored in the sparse array.| :white_check_mark: Yes|
|**indices**|`object`|Index array of size `count` that points to those accessor attributes that deviate from their initialization value. Indices must strictly increase.| :white_check_mark: Yes|
|**values**|`object`|Array of size `count` times number of components, storing the displaced accessor attributes pointed by [`indices`](#reference-indices). Substituted values must have the same `componentType` and number of components as the base accessor.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.



---------------------------------------
---------------------------------------
<a name="reference-target"></a>
# Target

The index of the node and TRS property that an animation channel targets.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**node**|`integer`|The index of the node to target.|No|
|**path**|`string`|The name of the node's TRS property to modify, or the "weights" of the Morph Targets it instantiates. For the "translation" property, the values that are provided by the sampler are the translation along the x, y, and z axes. For the "rotation" property, the values are a quaternion in the order (x, y, z, w), where w is the scalar. For the "scale" property, the values are the scaling factors along the x, y, and z axes.| :white_check_mark: Yes|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-texture"></a>
# Texture

A texture and its sampler.

**Related WebGL functions**: `createTexture()`, `deleteTexture()`, `bindTexture()`, `texImage2D()`, and `texParameterf()`

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**sampler**|`integer`|The index of the sampler used by this texture. When undefined, a sampler with repeat wrapping and auto filtering should be used.|No|
|**source**|`integer`|The index of the image used by this texture. When undefined, it is expected that an extension or other mechanism will supply an alternate texture source, otherwise behavior is undefined.|No|
|**name**|`string`|The user-defined name of this object.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.




---------------------------------------
---------------------------------------
<a name="reference-textureinfo"></a>
# TextureInfo

Reference to a texture.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**index**|`integer`|The index of the texture.| :white_check_mark: Yes|
|**texCoord**|`integer`|The set index of texture's TEXCOORD attribute used for texture coordinate mapping.|No, default: `0`|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.



---------------------------------------
---------------------------------------
<a name="reference-values"></a>
# Values

Array of size `accessor.sparse.count` times number of components storing the displaced accessor attributes pointed by `accessor.sparse.indices`.

**Properties**

|   |Type|Description|Required|
|---|----|-----------|--------|
|**bufferView**|`integer`|The index of the bufferView with sparse values. Referenced bufferView can't have ARRAY_BUFFER or ELEMENT_ARRAY_BUFFER target.| :white_check_mark: Yes|
|**byteOffset**|`integer`|The offset relative to the start of the bufferView in bytes. Must be aligned.|No, default: `0`|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.


---------------------------------------
---------------------------------------

* [Appendix A: Tangent Space Recalculation](#appendix-a-tangent-space-recalculation)

# Appendix A: Tangent Space Recalculation

**TODO**

# Appendix B: BRDF Implementation

*This section is non-normative.*

The glTF spec is designed to allow applications to choose different lighting implementations based on their requirements.

An implementation sample is available at https://github.com/KhronosGroup/glTF-Sample-Viewer/ and provides an example of a WebGL implementation of a standard BRDF based on the glTF material parameters.

As previously defined

`const dielectricSpecular = rgb(0.04, 0.04, 0.04)`
<br>
`const black = rgb(0, 0, 0)`

*c<sub>diff</sub>* = `lerp(baseColor.rgb * (1 - dielectricSpecular.r), black, metallic)`
<br>
*F<sub>0</sub>* = `lerp(dieletricSpecular, baseColor.rgb, metallic)`
<br>
*&alpha;* = `roughness ^ 2`

Additionally,  
*V* is the normalized vector from the shading location to the eye  
*L* is the normalized vector from the shading location to the light  
*N* is the surface normal in the same space as the above values  
*H* is the half vector, where *H* = normalize(*L*+*V*)  

The core lighting equation the sample uses is the Schlick BRDF model from [An Inexpensive BRDF Model for Physically-based Rendering](https://www.cs.virginia.edu/~jdl/bib/appearance/analytic%20models/schlick94b.pdf)

![](figures/lightingSum.PNG)

Below are common implementations for the various terms found in the lighting equation.

### Surface Reflection Ratio (F)

**Fresnel Schlick**

Simplified implementation of Fresnel from [An Inexpensive BRDF Model for Physically based Rendering](https://www.cs.virginia.edu/~jdl/bib/appearance/analytic%20models/schlick94b.pdf) by Christophe Schlick.

![](figures/lightingF.PNG)

### Geometric Occlusion (G)

**Smith Joint GGX**

[Understanding the Masking-Shadowing Function in Microfacet-Based BRDFs](http://jcgt.org/published/0003/02/03/paper.pdf) by Eric Heitz.

![](figures/lightingG.PNG)

### Microfacet Distribution (D)

**Trowbridge-Reitz**

Implementation of microfacet distrubtion from [Average Irregularity Representation of a Roughened Surface for Ray Reflection](https://www.osapublishing.org/josa/abstract.cfm?uri=josa-65-5-531) by T. S. Trowbridge, and K. P. Reitz

![](figures/lightingD.PNG)

### Diffuse Term (diffuse)

**Lambert**

Implementation of diffuse from [Lambert's Photometria](https://archive.org/details/lambertsphotome00lambgoog) by Johann Heinrich Lambert

![](figures/lightingDiff.PNG)

# Appendix C: Spline Interpolation

Animations in glTF support spline interpolation with a cubic spline.

The keyframes of a cubic spline in glTF have input and output values where each input value corresponds to three output values of the same type: in-tangent, data point, and out-tangent.

Given a set of keyframes

&nbsp;&nbsp;&nbsp;&nbsp;Input *t*<sub>*k*</sub> with Output in-tangent ***a***<sub>k</sub>, point ***v***<sub>*k*</sub>, and out-tangent ***b***<sub>k</sub> for *k* = 1,...,*n*

a spline segment between two keyframes is represented in a cubic Hermite spline form:

&nbsp;&nbsp;&nbsp;&nbsp;***p***(*t*) = (2*t*<sup>3</sup> - 3*t*<sup>2</sup> + 1)***p***<sub>0</sub> + (*t<sup>3</sup>* - 2*t*<sup>2</sup> + *t*)***m***<sub>0</sub> + (-2*t*<sup>3</sup> + 3*t*<sup>2</sup>)***p***<sub>1</sub> + (*t*<sup>3</sup> - *t*<sup>2</sup>)***m***<sub>1</sub>

where

&nbsp;&nbsp;&nbsp;&nbsp;*t* is a value between 0 and 1  
&nbsp;&nbsp;&nbsp;&nbsp;***p***<sub>0</sub> is the starting point at *t* = 0  
&nbsp;&nbsp;&nbsp;&nbsp;***m***<sub>0</sub> is the scaled starting tangent at *t* = 0  
&nbsp;&nbsp;&nbsp;&nbsp;***p***<sub>1</sub> is the ending point at *t* = 1  
&nbsp;&nbsp;&nbsp;&nbsp;***m***<sub>1</sub> is the scaled ending tangent at *t* = 1  
&nbsp;&nbsp;&nbsp;&nbsp;***p***(*t*) is the resulting point value  

and where at input offset *t*<sub>*current*</sub> with keyframe index *k*

&nbsp;&nbsp;&nbsp;&nbsp;*t* = (*t*<sub>*current*</sub> - *t*<sub>*k*</sub>) / (*t*<sub>*k*+1</sub> - *t*<sub>*k*</sub>)  
&nbsp;&nbsp;&nbsp;&nbsp;***p***<sub>0</sub> = ***v***<sub>*k*</sub>  
&nbsp;&nbsp;&nbsp;&nbsp;***m***<sub>0</sub> = (*t*<sub>*k*+1</sub> - *t*<sub>*k*</sub>)***b***<sub>k</sub>  
&nbsp;&nbsp;&nbsp;&nbsp;***p***<sub>1</sub> = ***v***<sub>*k*+1</sub>  
&nbsp;&nbsp;&nbsp;&nbsp;***m***<sub>1</sub> = (*t*<sub>*k*+1</sub> - *t*<sub>*k*</sub>)***a***<sub>k+1</sub>  

The scalar-point multiplications are per point component.

When the sampler targets a node's rotation property, the resulting ***p***(*t*) quaternion must be normalized before applying the result to the node's rotation.

> **Implementation Note:** When writing out rotation output values, exporters should take care to not write out values which can result in an invalid quaternion with all zero values. This can be achieved by ensuring the output values never have both -***q*** and ***q*** in the same spline.

> **Implementation Note:** The first in-tangent ***a***<sub>1</sub> and last out-tangent ***b***<sub>*n*</sub> should be zeros as they are not used in the spline calculations.






---------------------------------------
---------------------------------------


# Extensions

## KTX2

Based on code implementation


| Property | Type| Description | Required |
|:-----------------------| :--------------------------|:------------------------------------------| :--------------------------|
| `vkFormat` |`number`|   | Yes, Default: `0.0` |
| `pixelWidth` |`number`|  | Yes, Default: `1.0` |
| `pixelHeight` |`number`|  | Yes, Default: `0.0` |
| `pixelDepth` |`number`|  | Yes, Default: `0.0` |
| `layerCount` |`number`|  | Yes, Default: `0.0` |
| `levels` |`HeapLinkedList<Ktx2Level>`|  | Yes |
| `faceCount` |`number`|   | Yes, Default: `1.0` |
| `supercompressionScheme` |`number`|  | Yes, Default: `0.0` |
| `dfdByteOffset` |`number`|  | Yes, Default: `0.0` |
| `dfdByteLength` |`number`|  | Yes, Default: `0.0` |
| `sgdByteOffset` |`number`|  | Yes, Default: `0.0` |
| `generateMipmaps` |`bool`|  | Yes, Default: `true` |
| `metaData` |`KTXMetaData`|  | Yes |




---------------------------------------
---------------------------------------

## Light

All light types share the common set of properties listed below.

### Light Shared

| Property | Description | Required |
|:-----------------------|:------------------------------------------| :--------------------------|
| `name` | Name of the light. | No, Default: `""` |
| `color` | RGB value for light's color in linear space. | No, Default: `[1.0, 1.0, 1.0]` |
| `intensity` | Brightness of light in. The units that this is defined in depend on the type of light. `point` and `spot` lights use luminous intensity in candela (lm/sr) while `directional` lights use illuminance in lux (lm/m<sup>2</sup>) | No, Default: `1.0` |
| `type` | Declares the type of the light. | :white_check_mark: Yes |
| `range` | Hint defining a distance cutoff at which the light's intensity may be considered to have reached zero. Supported only for `point` and `spot` lights. Must be > 0. When undefined, range is assumed to be infinite. | No |


### Spot

When a light's `type` is `spot`, the `spot` property on the light is required. Its properties (below) are optional.

| Property | Description | Required |
|:-----------------------|:------------------------------------------| :--------------------------|
| `innerConeAngle` | Angle, in radians, from centre of spotlight where falloff begins. Must be greater than or equal to `0` and less than `outerConeAngle`. | No, Default: `0` |
| `outerConeAngle` | Angle, in radians, from centre of spotlight where falloff ends.  Must be greater than `innerConeAngle` and less than or equal to `PI / 2.0`. | No, Default: `PI / 4.0` |


### Image-Based Light

| Property | Description | Required |
|:-----------------------|:------------------------------------------| :--------------------------|
| `name` | Name of the light. | No |
| `rotation` | Quaternion that represents the rotation of the IBL environment. | No, Default: `[0.0, 0.0, 0.0, 1.0]` |
| `intensity` | Brightness multiplier for environment. | No, Default: `1.0` |
| `irradianceCoefficients` | Declares spherical harmonic coefficients for irradiance up to l=2. This is a 9x3 array. | :white_check_mark: Yes |
| `specularImages` | Declares an array of the first N mips of the prefiltered cubemap. Each mip is, in turn, defined with an array of 6 images, one for each cube face. i.e. this is an Nx6 array. | :white_check_mark: Yes |
| `specularImageSize` | The dimension (in pixels) of the first specular mip. This is needed to determine, pre-load, the total number of mips needed. | :white_check_mark: Yes |

### Texture Restrictions

- A glTF `texture` used for IBL cannot have a `KHR_texture_transform` extension defined.
- `specularEnvironmentTexture` and `diffuseEnvironmentTexture` (when used) must refer to a texture referring to a KTX2 image of **Cubemap** type as defined in KTX2, Section 4.3. Namely:
  - `pixelHeight` must be greater than 0.
  - `pixelDepth` must be 0.
  - `layerCount` must be 0.
  - `faceCount` must be 6.
- The image must contain mip levels.
- The transfer function for all image formats must be linear.
- Cubemaps orientation must be aligned with [glTF coordinate system](../../../../specification/2.0#coordinate-system-and-units). 




---------------------------------------
---------------------------------------

## Materials

## clearcoat

|   |Type|Description|Required|
|---|----|-----------|--------|
|**clearcoatFactor**|`number`|The clearcoat color factor.|No|
|**clearcoatTexture**|`object`|The base color texture.|No|
|**clearcoatRoughnessFactor**|`number`|The roughness of the material.|No|
|**clearcoatRoughnessTexture**|`object`|The clearcoat-roughness texture.|No|
|**clearcoatNormalTexture**|`object`|The clearcoat-normal texture.|No|
|**extensions**|`object`|Dictionary object with extension-specific objects.|No|
|**extras**|`any`|Application-specific data.|No|

Additional properties are allowed.

<br>
<br>

### pbrSpecularGlossiness

The following table lists the allowed types and ranges for the specular-glossiness model:

|   |Type|Description|Required|
|---|----|-----------|--------|
|**diffuseFactor** | `number[4]` | The reflected diffuse factor of the material.|No, default:`[1.0,1.0,1.0,1.0]`|
|**diffuseTexture** | [`textureInfo`](/specification/2.0/README.md#reference-textureInfo)  | The diffuse texture.|No|
|**specularFactor** | `number[3]` | The specular RGB color of the material. |No, default:`[1.0,1.0,1.0]`|
|**glossinessFactor** | `number` | The glossiness or smoothness of the material. |No, default:`1.0`|
|**specularGlossinessTexture** | [`textureInfo`](/specification/2.0/README.md#reference-textureInfo) | The specular-glossiness texture.|No|


<br>
<br>

The following table describes the expected rendering behavior based on the material definitions included in the asset:

| | Client supports metallic-roughness | Client supports metallic-roughness and specular-glossiness | 
|----|:----:|:----:|
|Asset has metallic-roughness | Render metallic-roughness | Render metallic-roughness |  
|Asset has metallic-roughness and specular-glossiness | Render metallic-roughness | Render specular-glossiness | 
|Asset has specular-glossiness with `extensionsRequired`| Fail to load | Render specular-glossiness | 
|Asset has specular-glossiness with `extensionsUsed` | Render as if no material | Render specular-glossiness | 

<br>
<br>


### Specular

The following table lists the allowed types and ranges for the specular-glossiness model:

|   |Type|Description|Required|
|---|----|-----------|--------|
|**specularFactor** | `number` | The specular RGB color of the material. |No|
|**specularGlossinessTexture** | [`textureInfo`](/specification/2.0/README.md#reference-textureInfo) | The specular texture.|No|

<br>
<br>

### unlit

The common Unlit material is defined by adding the
`KHR_materials_unlit` extension to any glTF material. When present, the
extension indicates that a material should be unlit and use available
`baseColor` values, alpha values, and vertex colors while ignoring all
properties of the default PBR model related to lighting or color. Alpha
coverage and doubleSided still apply to unlit materials.

```json
{
    "materials": [
        {
            "name": "MyUnlitMaterial",
            "pbrMetallicRoughness": {
                "baseColorFactor": [ 0.5, 0.8, 0.0, 1.0 ]
            },
            "extensions": {
                "KHR_materials_unlit": {}
            }
        }
    ]
}
```

#### Definition

The Unlit material model describes a constantly shaded surface that is
independent of lighting. The material is defined only by properties already
present in the [glTF 2.0 material specification](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#material).
No new properties are added by this extension — it is effectively a boolean
flag indicating use of an unlit shading model. Additional properties on the
extension object are allowed, but may lead to undefined behaviour in conforming
viewers.

Color is calculated as:

```
color = <baseColorTerm>
```

`<baseColorTerm>` is the product of `baseColorFactor`, `baseColorTexture`, and vertex color (if any), as defined by the [core glTF material specification](https://github.com/KhronosGroup/glTF/blob/master/specification/2.0/README.md#metallic-roughness-material).





---------------------------------------
---------------------------------------

## Textures

### Texture basisu

|   |Type|Description|Required|
|---|----|-----------|--------|
|**source** | `integer` | index of the images node which defines a reference to the KTX2 image with Basis Universal supercompression |yes|

<br>

### Texture astc hdr

|   |Type|Description|Required|
|---|----|-----------|--------|
|**source** | `integer` | index of the images node which defines a reference to the KTX2 image with ASTC HDR payload |yes|

<br>


### Texture bc6h

|   |Type|Description|Required|
|---|----|-----------|--------|
|**source** | `integer` | index of the images node which defines a reference to the KTX2 image with BC6H payload |yes|

<br>

### Texture Transform
The `KHR_texture_transform` extension may be defined on `textureInfo` structures. It may contain the following properties:

| Name       | Type       | Default      | Description
|------------|------------|--------------|---------------------------------
| `offset`   | `array[2]` | `[0.0, 0.0]` | The offset of the UV coordinate origin as a factor of the texture dimensions.
| `rotation` | `number`   | `0.0`        | Rotate the UVs by this many radians counter-clockwise around the origin. This is equivalent to a similar rotation of the image clockwise.
| `scale`    | `array[2]` | `[1.0, 1.0]` | The scale factor applied to the components of the UV coordinates.
| `texCoord` | `integer`  |              | Overrides the textureInfo texCoord value if supplied, and if this extension is supported.

Though this extension's values are unbounded, they will only produce sane results if the texture sampler's `wrap` mode is `REPEAT`, or if the result of the final UV transformation is within the range [0, 1] (i.e. negative scale settings and correspondingly positive offsets).

> **Implementation Note**: For maximum compatibility, it is recommended that exporters generate UV coordinate sets both with and without transforms applied, use the post-transform set in the texture `texCoord` field, then the pre-transform set with this extension. This way, if the extension is not supported by the consuming engine, the model still renders correctly. Including both will increase the size of the model, so if including the fallback UV set is too burdensome, either add this extension to `extensionsRequired` or use the same texCoord value in both places.

> **Implementation Note**: From the glTF core specification, the origin of the UV coordinates (0, 0) corresponds to the upper left corner of a texture image.
