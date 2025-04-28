
# COMP4037 Coursework 2 – Environmental Impact Visualization (Parallel Coordinates)
﻿
This repository contains an additional visualization for COMP4037 Research Methods Coursework 2, using **parallel coordinates plots** to analyze dietary environmental impacts by gender.
﻿
# Visualization
﻿
The insight is visualized using a **parallel coordinates plot**, created in Python with Matplotlib, Pandas, and Scikit-learn.  
It explores **environmental impacts**
﻿
# Key Insight
﻿
From the parallel coordinates plot, it is evident that **males generally have higher environmental impacts** compared to females across most diet groups.  
The **'meat'** and **'meat100'** male groups show significant spikes in greenhouse gas emissions and land use.  
Interestingly, the **gender difference is minimal** within the vegan group, indicating that adopting a **plant-based diet** reduces both **overall environmental burden** and **gender disparity**.
﻿
# Tools Used
﻿
- **Python**
- `pandas`
- `matplotlib`
- `sklearn` (for Min-Max scaling)
- Microsoft Word
- Microsoft PowerPoint

# Data Preparation Steps
﻿
- Selected seven key environmental indicators:
- Greenhouse Gas Emissions
- Agricultural Land Use
- Water Scarcity
- Eutrophication Potential
- Biodiversity Impact
- Water Use
- Acidification Potential
- Grouped data by **diet group** and **gender**, calculating mean values.
- Created a combined group label (e.g., `vegan_male`, `meat_female`).
- Applied **Min-Max normalization** (scaling all variables to [0,1]).
- Generated a **parallel coordinates plot** to display multivariate profiles.
﻿
# Author
﻿Xiaowei Shi 
