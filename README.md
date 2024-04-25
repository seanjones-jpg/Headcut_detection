## Geomorphological Data Processing Suite
This repository contains a comprehensive suite of tools and utilities designed to automate and streamline the processing of geomorphological data, with a particular focus on stream channel incision detection. Developed at Tomichi Creek Ecological Services, this suite aims to reduce manual surveying labor costs and enhance operational efficiency.
# Features

* Automated Stream Channel Incision Detection: The suite includes algorithms and techniques for automatically identifying and detecting stream channel incision, minimizing the need for manual surveying and analysis.
* Cost-Effective Solution: By automating the stream channel incision detection process, this suite has effectively reduced manual surveying labor costs by approximately $1,000,000, providing a significant cost-saving advantage.

# Getting Started

# Headcut Predictor

The `Headcut_Predictor` class provides functionality to predict locations of headcuts (areas of potential stream erosion) in a stream profile based on deviations from the average elevation change or slope change.

## Usage

1. Import the required classes:

```python
from new_dataframe import New_Dataframe
from headcut_predictor import Headcut_Predictor
```

2. Create an instance of the `New_Dataframe` class:

```python
new_df = New_Dataframe()
```

3. Load your stream profile data and create the final dataframe:

```python
datalist = ['path/to/stream_profile_1.csv', 'path/to/structure_1.csv', ...]
final_dataframe = new_df.create_final_dataframe(datalist)
```

The `create_final_dataframe` method processes the provided data files, calculates various stream profile metrics (slopes, sinuosity, deviation from average), and returns a `FinalDataFrame` object containing the consolidated dataframe and individual stream profiles.

4. Access the final dataframe and stream profiles:

```python
final_df = final_dataframe.final_df
stream_profiles = final_dataframe.stream_profiles
```

5. Create an instance of the `Headcut_Predictor` class:

```python
headcut_predictor = Headcut_Predictor()
```

6. Use the `elev_change_prediction` method to predict headcut locations based on elevation change deviation:

```python
stream_profile_name = 'stream_profile_1'
stream_df = stream_profiles[stream_profile_name]
max_allowable_deviation = 0.5  # Adjust as needed
predicted_df = headcut_predictor.elev_change_prediction(stream_df, max_allowable_deviation)
```

The `elev_change_prediction` method adds a new column 'Exceeds Dev' to the input dataframe, where a value of 1 indicates a potential headcut location based on the specified maximum allowable deviation from the average elevation change.

7. Use the `slope_change_prediction` method to predict headcut locations based on slope change deviation:

```python
slope_gap_title = 'Slope Gap: 1'  # Adjust as needed
max_allowable_deviation = 0.5  # Adjust as needed
predicted_df = headcut_predictor.slope_change_prediction(stream_df, slope_gap_title, max_allowable_deviation)
```

The `slope_change_prediction` method adds a new column 'Exceeds Slope Dev' to the input dataframe, where a value of 1 indicates a potential headcut location based on the specified maximum allowable deviation from the average slope change for the given slope gap.

8. Use the `filter_bools` method to obtain a filtered dataframe containing only the potential headcut locations:

```python
bool_col = 'Exceeds Dev'  # or 'Exceeds Slope Dev'
headcut_locations_df = headcut_predictor.filter_bools(predicted_df, bool_col)
```

The `filter_bools` method returns a new dataframe containing only the rows where the specified boolean column (`bool_col`) has a value of 1.

9. Visualize the stream profiles and potential headcut locations using the `Visualize_Profile` class:

```python
from visualize_profile import Visualize_Profile

viz = Visualize_Profile()
viz.plot_elev_profile(predicted_df, 'Stream Profile', show_structures=True, bool_col=bool_col)
viz.plot_zoomed_profiles(predicted_df, 'Stream Profile', bool_col=bool_col)
```

The `plot_elev_profile` method plots the elevation profile of the stream, highlighting the potential headcut locations if `show_structures` is set to `True`.

The `plot_zoomed_profiles` method plots zoomed-in sections of the elevation profile around the potential headcut locations.

By following these steps, you can load your stream profile data, predict headcut locations based on elevation change or slope change deviations, filter the potential headcut locations, and visualize the results.
