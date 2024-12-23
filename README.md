# object-localization

## Overview
This project identifies a specific object in an image using keypoint matching and geometric transformations. It outputs the object's position, size, and orientation based on a reference image. The solution can locate any object given a proper reference image.

## Input and Output
- Input images: 2000x1500 pixels.
- Reference image: `reference.png` in the current directory.
- Program reads the test image path from standard input and outputs:
  - `X Y H A`: Center coordinates (`X`, `Y`), height (`H`), and angle (`A`) of the bounding box.

Example Output:
```
1186 725 615 0
```

## Constraints
1. The object's orientation varies from -90° to 90°.
2. Bounding box width is 60% of its height.
3. Occlusion is <30%.
4. Execution time per image: <20 seconds.
5. Environment: 4 CPUs, 6GB RAM.

## Implementation
### Steps
1. **Keypoint Matching:**
   - Extracts SIFT keypoints and descriptors.
   - Matches descriptors using a ratio test and mutual nearest neighbors.
2. **Transformation Matrix:**
   - Computes an affine transformation via RANSAC.
   - Applies transformation to map the reference bounding box to the test image.
3. **Bounding Box:**
   - Calculates center (`X`, `Y`), height (`H`), and orientation (`A`).

### Components
#### `main.py`
1. Loads reference and test images.
2. Matches keypoints and estimates a transformation matrix.
3. Transforms and calculates bounding box parameters.
4. Outputs the results.

#### Helper Functions
- **`match_descriptors()`**: Matches descriptors with ratio test.
- **`compute_best_transformation()`**: Estimates transformation using RANSAC.
- **`compute_obb()`**: Calculates oriented bounding box from transformed points.

### Example Workflow
1. Place `reference.png` in the current directory.
2. Run the program:
   ```bash
   python main.py < /path/to/test/image.png
   ```
3. Output example:
   ```
   1186 725 615 0
   ```


This implementation balances robustness and speed, leveraging geometric transformations and keypoint matching to accurately locate the object under varied conditions.

