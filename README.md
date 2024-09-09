# db_survey 
by
Lorenzo Orlandi,
Daniele Sevengnani,
Nicola Conci

This work is the result of the collaboration between **Arcoda s.r.l.** and the group **MMLab**

This research is supported by the project **DIMOTY**, funded by the Autonomous Province of Trento under the **LP6/99** framework


## Overview

The `db_survey` dataset consists of high-precision georeferenced images captured in various excavation scenarios. The dataset is designed for use in research and analysis related to surveying, mapping, and geospatial applications. The images are georeferenced with centimeter-level accuracy, and the GPS data is embedded directly in the EXIF metadata of each image.

The dataset includes:
- **10 excavation scenarios**
- **4 park scenarios** (part of the outdoor scenarios)
- **2 indoor scenarios**

Each image has a resolution of **1280x720 pixels** and is stored in formats suitable for geospatial analysis.

## Dataset Composition

1. **Excavation Scenarios**
   - **Total**: 10 scenarios
   - **Description**: Georeferenced images of excavation sites with high precision. These images are useful for detailed analysis of terrain, structures, and other physical characteristics of excavation areas.
   - **GPS Data**: Embedded in EXIF metadata for each image.

2. **Outdoor Scenarios (Including Park Scenarios)**
   - **Total**: 4 park scenarios, as part of the outdoor scenarios.
   - **Description**: These scenarios cover park areas with natural and man-made features, providing a detailed view of open outdoor spaces.
   - **Georeferencing**: The images are georeferenced with centimeter-level accuracy, with GPS coordinates stored in EXIF metadata.

3. **Indoor Scenarios**
   - **Total**: 2 indoor scenarios
   - **Description**: Indoor scenarios include detailed imagery of enclosed spaces, capturing various structures, equipment, and environments under controlled lighting and conditions.
   - **GPS Data**: Even though these scenarios are indoors, georeferenced data is included where applicable.

## Image Specifications

- **Resolution**: 1280x720 pixels
- **Georeferencing**: Centimeter-level accuracy
- **GPS Data**: Embedded in EXIF metadata for easy extraction
- **Formats**: Images are provided in standard formats (e.g., GeoTIFF, JPEG with EXIF) for easy integration into geospatial software.

### Example of EXIF GPS Data Extraction

If you need to extract the GPS data from the images, it is stored directly in the EXIF metadata. Here's an example of how to extract it in Python using the `PIL` and `exif` libraries:

```python
from PIL import Image
from PIL.ExifTags import TAGS, GPSTAGS

def get_gps_info(image_file):
    image = Image.open(image_file)
    exif_data = image._getexif()

    if exif_data:
        for tag, value in exif_data.items():
            tag_name = TAGS.get(tag, tag)
            if tag_name == "GPSInfo":
                gps_info = {}
                for t in value:
                    gps_tag = GPSTAGS.get(t, t)
                    gps_info[gps_tag] = value[t]
                return gps_info
    return None

# Example usage
image_file = 'path_to_your_file/image_file.jpg'
gps_info = get_gps_info(image_file)

if gps_info:
    print("GPS Data:", gps_info)
else:
    print("No GPS data found")
