Topology Validation Test Cases
==============================

A JSON port of the validation suite originally provided by JTS, the
[Java Topology Suite](http://www.vividsolutions.com/jts/JTSHome.htm). This
repository contains all 575 test cases in an easy-to-use JSON format.

## Format

Each case contains one or two geometries (in the original WKT format as well as
GeoJSON) and the associated spatial relationships and of spatial analysis
results.

Within the JSON file, there is a root `cases` property that contains an array
of test cases with the following structure.


* **`id`** - unique identifier for each case
* **`category`** - category of the test case (one of `function`, `relate`, `unary`)
* **`group`** - group that the test case belongs to (such as `TestFunctionPL`
                denoting a group of test cases related to the functions between
                a Point and a Line)
* **`title`** - descriptive title for the case
* **`a`** - geometry A, including a WKT representation (`wkt`) and a GeoJSON
               representation (`geometry`)
* **`b`** (if present) - same as wktA (not present in test cases of type `unary`
* **`relationship`** - When two geometries are given, this will contain the named
                       spatial predicates and their results for the two geometries
                       and the Dimensionally Extended nine-Intersection Model
                       ([DE-9IM](https://en.wikipedia.org/wiki/DE-9IM)) representation
                       of the relationship.
* **`functions`** - The result of a selection of spatial analysis functions are
                    included in WKT and GeoJSON representation.

## Example

Sample test case containing two polygons.  See the original JTS visualization
[here](http://www.vividsolutions.com/jts/tests/Run14Case3.html).

```json
{
  "id": "14-003",
  "category": "function",
  "group": "TestFunctionAA",
  "title": "AA - simple polygons #2",
  "a": {
    "wkt": "POLYGON ((20 340, 330 380, 50 40, 20 340))",
    "geometry": {
      "type": "Polygon",
      "coordinates": [[[20, 340], [330, 380], [50,40], [20, 340]]]
    }
  },
  "b": {
    "wkt": "POLYGON ((210 320, 140 270, 0 270, 140 220, 210 320))",
    "geometry": {
      "type": "Polygon",
      "coordinates": [[[210, 320], [140, 270], [0, 270], [140, 220], [210, 320]]]
    }
  },
  "relationship": {
    "equals": false,
    "disjoint": false,
    "intersects": true,
    "touches": false,
    "crosses": false,
    "within": false,
    "contains": false,
    "overlaps": true,
    "de9im": "212101212"
  },
  "functions": {
    "convexHull": {
      "wkt": "POLYGON ((50 40, 20 340, 330 380, 50 40))",
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[50, 40], [20, 340], [330, 380], [50, 40]]]
      }
    },
    "intersection": {
      "wkt": "POLYGON ((28 260, 27 270, 140 270, 210 320, 140 220, 28 260))",
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[28, 260], [27, 270], [140, 270], [210, 320], [140, 220], [28, 260]]]
      }
    },
    "union": {
      "wkt": "POLYGON ((20 340, 330 380, 50 40, 28 260, 0 270, 27 270, 20 340))",
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[20, 340], [330, 380], [50, 40], [28, 260], [0, 270], [27, 270], [20, 340]]]
      }
    },
    "difference": {
      "wkt": "POLYGON ((20 340, 330 380, 50 40, 28 260, 140 220, 210 320, 140 270, 27 270, 20 340))",
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[20, 340], [330, 380], [50, 40], [28, 260], [140, 220], [210, 320], [140, 270], [27, 270], [20, 340]]]
      }
    },
    "symDifference": {
      "wkt": "MULTIPOLYGON (((20 340, 330 380, 50 40, 28 260, 140 220, 210 320, 140 270, 27 270, 20 340)),((27 270, 28 260, 0 270, 27 270)))",
      "geometry": {
        "type": "MultiPolygon",
        "coordinates": [[[[20, 340], [330, 380], [50, 40], [28, 260], [140, 220], [210, 320], [140, 270], [27, 270], [20, 340]]], [[[27, 270], [28, 260], [0, 270], [27, 270]]]]
      }
    }
  }
}
```
