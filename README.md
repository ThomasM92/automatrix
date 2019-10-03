
![Ellisetting](https://ellistat.com/wp-content/uploads/2018/04/Ellisetting_logo_72dpi.png)

# Automatrix <a name="tableofcontent"></a>

- [ **About** ]( #about )
- [ **Tools** ]( #tools )
- [ **Frames** ]( #frames )
- [ **Dimensions** ]( #dimensions )
- [ **Geometries** ]( #geometries )

<br/>

## [ About <a name="about"></a> ]( #tableofcontent )

This module allow the automatic construction of the piloting matrix (linking dimensions to correctors) for multidimensional process control.

| Field      | Type       | Description                                             |
| ---------- | ---------- | ------------------------------------------------------- |
| geometries | `object[]` | all the CAD objects and their links between each others |
| dimensions | `object[]` | the dimensions and their links to geometries            |
| frames     | `object[]` | the different frames in which the tools work            |
| tools      | `object[]` | the tools and their links to geometries they work       |

<br/>

## [ Tools <a name="tools"></a> ]( #tableofcontent )

#### Description

The **Tools** array reference all the tools and their links to the local frames in which they operate and to the geometries they work.
Tools of type `FLAT`, `BALL` and `SHAPE` are supported.

#### Structure

```
.
├── id : STRING
├── type : STRING
└── links : OBJECT[]
    ├── link_1 : OBJECT
    │   ├── geometry_id : STRING
    │   ├── frame_id : STRING
    │   └── direction : NUMBER[]
    .
```

#### Fields

| Field       | Type       | Description                                                  |
| ----------- | ---------- | ------------------------------------------------------------ |
| id          | `string`   | the tool's identifier                                        |
| type        | `string`   | the tool's type                                              |
| links       | `object[]` | array of link objects                                        |
| geometry_id | `string`   | this link's geometry identifier                              |
| frame_id    | `string`   | identifier of the local frame in which the tool work         |
| direction   | `number[]` | the tool tip direction in the local frame                    |

#### Example

```json
{
    "id": "tool1",
    "type": "FLAT",
    "links": [
        {
            "frame_id": "#G55",
            "geometry_id": "#123",
            "direction": [ 0, 0, 1 ]
        },
        ...
    ]
},
```

<br/>

## [ Frames <a name="frames"></a> ]( #tableofcontent )

#### Description

The **Frames** array reference all the local frames in which the tools work.

#### Structure

```
.
├── id : STRING
└── axis_system : OBJECT
    ├── Ox : NUMBER[]
    ├── Oy : NUMBER[]
    └── Oz : NUMBER[]
```

#### Fields

| Field       | Type       | Description                                                  |
| ----------- | ---------- | ------------------------------------------------------------ |
| id          | `string`   | the tool's identifier                                        |
| axis_system | `object`   | expression of the local frame in the reference frame         |
| Oz          | `number[]` | Ox vector                                                    |
| Oy          | `number[]` | Oy vector                                                    |
| Ox          | `number[]` | Oz vector                                                    |

#### Example

```json
{
	"id": "G55",
    "axis_system": {
        "Ox": [ 1, 0, 0 ],
        "Oy": [ 0, 0, 1 ],
        "Oz": [ 0, -1, 0 ]
    }
},
```

<br/>

## [ Dimensions <a name="dimensions"></a> ]( #tableofcontent )

#### Description

The **Dimensions** array reference all the dimensions and their links to their associated geometries.
Dimensions of type `LINEAR`, `RADIUS`, `DIAMETER`, `ANGULAR` and `SYMMETRY` are supported.

#### Structure

```
.
├── id : STRING
├── type : STRING
└── links : STRING[]
```

#### Fields

| Field       | Type       | Description                                            |
| ----------- | ---------- | ------------------------------------------------------ |
| id          | `string`   | the dimension's identifier                             |
| type        | `string`   | the dimension's type                                   |
| links       | `object[]` | identifiers of the geometries linked to the dimension  |

#### Example

```json
{
    "id" : "#123",
    "type" : "LINEAR",
    "links" : [ "#312", "#231"]
}
```

<br/>

## [ Geometries <a name="geometries"></a> ]( #tableofcontent )

#### Description

The **Geometries** array reference all the geometries and their links between each other.
Geometries of type `PLANE`, `CYLINDRICAL SURFACE`, `SPLINE SURFACE`, `SPLINE CURVE`, `CIRCLE`, `LINE` and `POINT` are supported.


#### Structure

```
.
├── id : STRING
├── type : STRING
├── data : OBJECT[]
├── position : NUMBER[]
├── direction : NUMBER[]
└── links : STRING[]
```

#### Fields

| Field       | Type       | Description                                     |
| ----------- | ---------- | ----------------------------------------------- |
| id          | `string`   | the geometry's identifier                       |
| type        | `string`   | the geometry's type                             |
| position    | `number[]` | position of the geometry                        |
| direction   | `number[]` | direction of the geometry                       |
| data        | `object[]` | other CAD data specific to the geometry type    |
| links       | `string[]` | array of node geometries linked to this surface |

#### Examples

```json
{
    "id": "#167",
    "type": "PLANE",
    "position": [0, 0, 0],
    "direction": [-0, -1, -0],
    "sens": false,
    "links": [
        "#123",
        "#312",
        "#231",
        ...
    ]
}
```

```json
{
    "id": "#188",
    "type": "CIRCLE",
    "position": [0.25, 0.51, 0.16],
    "direction": [1, 0, 0],
    "data": {
        "start": [0.25, 0.6, 0.16],
        "end": [0.25, 0.51, 0.25],
        "radius": 1
        ...
    },
}
```
