import pandas as pd
import matplotlib.pyplot as plt
from pandas.plotting import parallel_coordinates
from sklearn.preprocessing import MinMaxScaler

# read data
df = pd.read_csv('Results_21MAR2022_nokcaladjust.csv')

# Select the required columns
selected_columns = [
    'diet_group', 'sex',
    'mean_ghgs', 'mean_land', 'mean_watscar',
    'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid'
]
df_selected = df[selected_columns]

# Take the mean by dietary type and gender grouping
df_grouped = df_selected.groupby(['diet_group', 'sex']).mean().reset_index()

# Create a new column combination name group
df_grouped['group'] = df_grouped['diet_group'] + '_' + df_grouped['sex']

# Normalization processing
scaler = MinMaxScaler()
features_scaled = scaler.fit_transform(df_grouped[
    ['mean_ghgs', 'mean_land', 'mean_watscar', 'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid']
])
df_scaled = pd.DataFrame(features_scaled, columns=[
    'mean_ghgs', 'mean_land', 'mean_watscar', 'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid'
])
df_scaled['group'] = df_grouped['group']

# Draw a parallel coordinate graph
plt.figure(figsize=(14, 8))
parallel_coordinates(df_scaled, 'group', colormap='cool', linewidth=2)
plt.title('Environmental Impact across Diet Groups and Gender (Parallel Coordinates)', fontsize=16)
plt.xlabel('Environmental Indicators', fontsize=12)
plt.ylabel('Normalized Impact', fontsize=12)
plt.xticks(rotation=45)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()

# Display image
plt.show()

# Optional Save Image
# plt.savefig('parallel_coordinates_sex_diet_impact.png')
