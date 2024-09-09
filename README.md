# db_survey 
by
Lorenzo Orlandi,
Giulia Bruscagin,
Daniele Sevengnani,
Nicola Conci

This work is the result of the collaboration between **Arcoda s.r.l.** and the group **MMLab**

This research is supported by the project **DIMOTY**, funded by the Autonomous Province of Trento under the **LP6/99** framework


## Overview

The `db_survey` dataset consists of high-precision georeferenced images captured in various scenarios, with a focus on outdoor environments. The dataset is designed for research and analysis in fields like surveying, mapping, and geospatial applications. The images are georeferenced with centimeter-level accuracy, and the GPS data is embedded directly in the EXIF metadata of each image.

Where possible, the images have been captured in an **object-centric** manner, focusing on specific objects of interest to ensure detailed and centered perspectives.

- **Dataset Size**: Outdoor 4.25 GB + Indoor 0.328 GB 
- **[Download the `db_survey` dataset](https://arcodagis-my.sharepoint.com/:f:/g/personal/giulia_bruscagin_arcoda_it/EhZJUU1lfvVPt_WiBi6QPBsBCAXuHMRH9rZFVhKyXPiU6w?e=yY4hN1)

The dataset includes:
- **10 outdoor excavation scenarios**
- **4 park scenarios** (part of the outdoor environments)
- **2 indoor scenarios**

Each image has a resolution of **1280x720 pixels** and is stored in formats suitable for geospatial analysis.

## Dataset Composition

1. **Outdoor Scenarios**
   - **Total**: 14 outdoor scenarios, which include:
     - **Excavation Scenarios**: 10 scenarios focusing on excavation sites.
     - **Park Scenarios**: 4 scenarios capturing different sections of park areas.
   - **Description**: The outdoor scenarios feature natural and man-made landscapes, including detailed imagery of excavation sites and parks. These scenarios provide useful geospatial data for analyzing terrain, vegetation, and other physical structures.
   - **GPS Data**: Embedded in EXIF metadata for each image.
   - **Acquisition Mode**: Object-centric where possible, with attention to key objects of interest, such as excavation artifacts or park features.

2. **Indoor Scenarios**
   - **Total**: 2 indoor scenarios
   - **Description**: The indoor scenarios include imagery of enclosed spaces, featuring different structures, equipment, and environments under controlled lighting conditions.
   - **GPS Data**: Georeferenced data is included where applicable.
   - **Acquisition Mode**: Object-centric focus on interior elements of interest.

## Image Specifications

- **Resolution**: 1280x720 pixels
- **Georeferencing**: Centimeter-level accuracy(Outdoor scenario), Reconstructed with Vi-Slam (Indoor Scenario) Embedded in EXIF metadata for easy extraction
- **Acquisition Method**: Object-centric captures where possible
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
