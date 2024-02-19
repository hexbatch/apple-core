# Locations are geo json

see https://datatracker.ietf.org/doc/html/rfc7946

* 2-dimensional shapes are always lat and lng
* 3-dimensional shapes are any number

Either polygons or multipolygons can be used for 2d and 3d

# Polygons

    {
        "type": "Polygon",
        "coordinates": [
            [
                [
                    -91.23046875,
                    45.460130638
                ],
                [
                    -79.8046875,
                    49.837982453
                ],
                [
                    -69.08203125,
                    43.452918894
                ],
                [
                    -88.2421875,
                    32.694865978
                ],
                [
                    -91.23046875,
                    45.460130638
                ]
            ]
        ]
    }

# multi polygons

        {
            "type": "MultiPolygon",
            "coordinates": [
                [
                   [ [0, 0, 0], [100, 0, 0], [100, 100, 0], [0, 100, 0], [0, 0, 100], [100, 0, 100], [100, 100, 100], [0, 100, 100],[0, 0, 0] ]
                ],
                 [
                   [ [0, 0, 0], [-100, 0, 0], [-100, -100, 0], [0, -100, 0], [0, 0, -100], [-100, 0, -100], [-100, -100, -100], [0, -100, -100],[0, 0, 0] ]
                ]
            ]
        }
