import pandas as pd
import matplotlib.pyplot as plt
from pandas.plotting import parallel_coordinates
from sklearn.preprocessing import MinMaxScaler

# 读取数据
df = pd.read_csv('Results_21MAR2022_nokcaladjust.csv')

# 选取需要的列
selected_columns = [
    'diet_group', 'sex',
    'mean_ghgs', 'mean_land', 'mean_watscar',
    'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid'
]
df_selected = df[selected_columns]

# 按饮食类型和性别分组取均值
df_grouped = df_selected.groupby(['diet_group', 'sex']).mean().reset_index()

# 创建新列组合名称 group
df_grouped['group'] = df_grouped['diet_group'] + '_' + df_grouped['sex']

# 归一化处理
scaler = MinMaxScaler()
features_scaled = scaler.fit_transform(df_grouped[
    ['mean_ghgs', 'mean_land', 'mean_watscar', 'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid']
])
df_scaled = pd.DataFrame(features_scaled, columns=[
    'mean_ghgs', 'mean_land', 'mean_watscar', 'mean_eut', 'mean_bio', 'mean_watuse', 'mean_acid'
])
df_scaled['group'] = df_grouped['group']

# 绘制平行坐标图
plt.figure(figsize=(14, 8))
parallel_coordinates(df_scaled, 'group', colormap='cool', linewidth=2)
plt.title('Environmental Impact across Diet Groups and Gender (Parallel Coordinates)', fontsize=16)
plt.xlabel('Environmental Indicators', fontsize=12)
plt.ylabel('Normalized Impact', fontsize=12)
plt.xticks(rotation=45)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()

# 显示图
plt.show()

# 可选保存图
# plt.savefig('parallel_coordinates_sex_diet_impact.png')
