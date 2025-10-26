# NBA Players Visualization

## Stephen Curry vs Kyrie Irving and LeBron James vs Carmelo Anthony

---

## Abstract

This project presents comprehensive data visualizations for analyzing NBA player performance across multiple dimensions. By comparing elite players like Stephen Curry vs Kyrie Irving and LeBron James vs Carmelo Anthony, we provide insights into shooting patterns, scoring efficiency, and overall gameplay styles. The visualizations serve as powerful tools for team managers, scouts, and coaches to make informed decisions about player recruitment, training, and game strategy.

---

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Data Source](#data-source)
- [Visualization Types](#visualization-types)
- [Installation](#installation)
- [Usage](#usage)
- [Key Insights](#key-insights)
- [Technologies Used](#technologies-used)
- [Future Directions](#future-directions)
- [References](#references)

---

## Introduction

Data visualization transforms complex NBA statistics into actionable insights. This project focuses on:

- **Player Comparison:** Direct statistical comparison between players in similar positions
- **Performance Analysis:** Multi-dimensional evaluation of scoring, assists, rebounds, and shooting efficiency
- **Strategic Insights:** Identifying player strengths, weaknesses, and optimal court zones
- **Interactive Exploration:** Dynamic dashboards for real-time data exploration

The visualizations help answer critical questions:
- Which zones on the court does each player dominate?
- How do shooting percentages vary by distance and location?
- What is the relationship between playing time and performance?
- How have players evolved across seasons?

---

## Features

### Shot Analysis
- **Shot Charts:** Hit/miss visualization on basketball court with actual dimensions
- **Hex Maps:** Hexagonal binning for shot density and efficiency analysis
- **Zone Analysis:** Performance breakdown by court zones and distances
- **Heat Maps:** Concentration patterns of shooting locations

### Performance Metrics
- **Points Per Game:** Season-by-season scoring trends
- **Rebounds Per Game:** Offensive and defensive rebounding analysis
- **Assists Per Game:** Playmaking capabilities visualization
- **Field Goal Percentage:** Shooting efficiency across various metrics

### Advanced Visualizations
- **3D Plots:** Multi-dimensional performance analysis (Points, Rebounds, Assists)
- **Correlation Matrices:** Relationship between different statistical categories
- **Interactive Dashboards:** User-driven exploration with filters and controls
- **Animated Visualizations:** Time-series performance tracking
- **Density Plots:** Distribution analysis of key statistics

### Comparative Analysis
- **Side-by-Side Comparisons:** Direct player matchups
- **Joint Plots:** Correlation with marginal distributions
- **Box & Scatter Combinations:** Statistical distribution with outlier detection
- **Beeswarm Plots:** Dense information display for game-by-game performance

---

## Data Source

Data is sourced using the **nba_api** Python package, which provides access to official NBA.com statistics:

```python
from nba_api.stats.endpoints import playercareerstats

# Example: Fetch Stephen Curry's career stats
career = playercareerstats.PlayerCareerStats(player_id='201939')
```

### Player IDs
- **Stephen Curry:** 201939
- **Kyrie Irving:** 202681
- **LeBron James:** 2544
- **Carmelo Anthony:** 2546

### Data Categories
- Career statistics (season-by-season)
- Shot location data (x, y coordinates)
- Game-by-game performance
- Advanced metrics (usage %, true shooting %, etc.)

---

## Visualization Types

### 1. Shot Charts
Scatter plots overlaid on basketball court showing:
- Green circles: Made shots
- Red crosses: Missed shots
- Court drawn with accurate NBA dimensions

### 2. Hex Maps
Hexagonal binning for:
- Shot density visualization
- Efficiency by location
- Reduced noise compared to scatter plots

### 3. Heat Maps
Color-intensity maps showing:
- Shot concentration areas
- High-efficiency zones
- Using 'inferno' colormap for clarity

### 4. Statistical Plots
- **Line Plots:** Trends over seasons
- **Bar Plots:** Categorical comparisons
- **Scatter Plots:** Relationship between variables
- **Box Plots:** Distribution and outliers
- **Pie Charts:** Proportional breakdowns

### 5. Interactive Elements
- Dropdown menus for player selection
- Slider bars for season filtering
- Hover tooltips for detailed stats
- Animated transitions between seasons

---

## Example of Visualizations Created

<img width="628" height="449" alt="Screenshot 2025-10-26 at 2 23 58 PM" src="https://github.com/user-attachments/assets/3c17c5ad-a7cc-40ce-9ff0-43f02645c1dc" />

<img width="1241" height="751" alt="Screenshot 2025-10-26 at 2 24 18 PM" src="https://github.com/user-attachments/assets/60938206-2334-494c-8c86-fb698b8c26c5" />

<img width="1190" height="737" alt="Screenshot 2025-10-26 at 2 24 34 PM" src="https://github.com/user-attachments/assets/f90689a1-4b31-4a6e-a5a3-812ae828565b" />

<img width="1268" height="929" alt="Screenshot 2025-10-26 at 2 24 48 PM" src="https://github.com/user-attachments/assets/cf522400-12eb-416e-973a-782ddaeb184b" />

<img width="1508" height="753" alt="Screenshot 2025-10-26 at 2 25 01 PM" src="https://github.com/user-attachments/assets/24b799e9-2906-4965-a79f-2be29c1e713e" />

---

## Installation

### Prerequisites
```bash
Python 3.7+
pip package manager
```

### Required Libraries
```bash
pip install nba_api
pip install pandas numpy
pip install matplotlib seaborn plotly
pip install scipy
```

### Optional (for enhanced visualizations)
```bash
pip install jupyter notebook
pip install ipywidgets
```

---

## Usage

### Basic Analysis
```python
# Import required libraries
from nba_api.stats.endpoints import playercareerstats, shotchartdetail
import matplotlib.pyplot as plt
import seaborn as sns

# Fetch player data
curry_stats = playercareerstats.PlayerCareerStats(player_id='201939')
curry_df = curry_stats.get_data_frames()[0]

# Create basic visualization
plt.figure(figsize=(12, 8))
plt.plot(curry_df['SEASON_ID'], curry_df['PTS'], marker='o')
plt.title('Stephen Curry - Points Per Season')
plt.xlabel('Season')
plt.ylabel('Total Points')
plt.show()
```

### Shot Chart Creation
```python
# Fetch shot chart data
shot_data = shotchartdetail.ShotChartDetail(
    team_id=0,
    player_id='201939',
    season_nullable='2022-23',
    context_measure_simple='FGA'
)

shots_df = shot_data.get_data_frames()[0]

# Plot shots on court (simplified)
plt.figure(figsize=(12, 11))
made = shots_df[shots_df['SHOT_MADE_FLAG'] == 1]
missed = shots_df[shots_df['SHOT_MADE_FLAG'] == 0]

plt.scatter(made['LOC_X'], made['LOC_Y'], 
           c='green', marker='o', alpha=0.5, label='Made')
plt.scatter(missed['LOC_X'], missed['LOC_Y'], 
           c='red', marker='x', alpha=0.5, label='Missed')
plt.legend()
plt.show()
```

---

## Key Insights

### Stephen Curry vs Kyrie Irving

**Stephen Curry:**
- Field Goal %: 50.4%
- Elite 3-point shooter with majority of shots from beyond the arc
- Excellent buzzer-beater record
- Strong in center and right-side zones
- Higher assists per game across most seasons

**Kyrie Irving:**
- Field Goal %: 44.8%
- Exceptional inside-the-arc playmaker
- Superior shot completion ability under pressure
- Consistent across all court zones
- Lower 3-point attempts but solid efficiency

**Key Takeaway:** Curry excels as a perimeter shooter, while Irving dominates with inside scoring and playmaking.

---

### LeBron James vs Carmelo Anthony

**LeBron James:**
- Field Goal %: 52.1%
- All-around player with balanced inside/outside game
- Dominant in rebounds and assists
- Strong left-side and center zone performance
- Consistent scoring across all distances

**Carmelo Anthony:**
- Field Goal %: 43.4%
- Elite 3-point shooting specialist
- Primarily right-side court strength
- Lower rebounding and assist numbers
- Peak performance in specific seasons

**Key Takeaway:** LeBron demonstrates all-around excellence, while Carmelo specializes in perimeter scoring.

---

## Technologies Used

### Python Libraries
- **nba_api:** Official NBA data access
- **pandas:** Data manipulation and analysis
- **numpy:** Numerical computations
- **matplotlib:** Static visualizations
- **seaborn:** Statistical graphics
- **plotly:** Interactive visualizations
- **scipy:** Statistical analysis

### Visualization Techniques
- Scatter plots with custom markers
- Hexagonal binning (hexbin)
- Heat maps with custom colormaps
- 3D surface plots
- Animated time-series
- Interactive dashboards
- Correlation matrices

---

## Future Directions

### Planned Enhancements

1. **Multi-Sport Extension**
   - Adapt visualizations for soccer, cricket, baseball
   - Sport-specific metrics and court/field layouts

2. **Real-Time Analysis**
   - Live game visualization during matches
   - Half-time performance reports
   - In-game strategy adjustments

3. **Movement Tracking**
   - Player positioning heatmaps
   - Movement patterns and speed analysis
   - Defensive coverage visualization

4. **International Competitions**
   - Olympic basketball analysis
   - FIBA World Cup statistics
   - Cross-league comparisons

5. **Machine Learning Integration**
   - Performance prediction models
   - Injury risk assessment
   - Optimal lineup recommendations

6. **Enhanced Interactivity**
   - Web-based dashboard deployment
   - Mobile app development
   - Real-time data streaming

---

## Project Structure

```
NBA-Visualization/
│
├── data/
│   ├── raw/                 # Raw API data
│   └── processed/           # Cleaned datasets
│
├── notebooks/
│   ├── data_collection.ipynb
│   ├── curry_vs_irving.ipynb
│   └── lebron_vs_carmelo.ipynb
│
├── src/
│   ├── data_fetcher.py      # API data collection
│   ├── court_drawer.py      # Basketball court rendering
│   ├── visualizations.py    # Core plotting functions
│   └── analysis.py          # Statistical analysis
│
├── outputs/
│   ├── figures/             # Generated visualizations
│   └── reports/             # Analysis reports
│
├── requirements.txt         # Python dependencies
├── README.md               # This file
└── LICENSE
```

---

## Methodology

### Data Collection
1. Player identification via NBA API player IDs
2. Career statistics extraction (all seasons)
3. Shot-level data collection (location, outcome)
4. Advanced metrics calculation

### Data Processing
1. Missing value handling
2. Normalization by games played
3. Zone and distance categorization
4. Statistical aggregation

### Visualization Design
1. Appropriate chart type selection based on data characteristics
2. Color encoding following perceptual principles
3. Interactive elements for user exploration
4. Responsive design for different display sizes

---

## Limitations and Considerations

### Data Limitations
- API rate limits may affect bulk data collection
- Historical data availability varies by metric
- Shot location precision dependent on tracking technology

### Visualization Choices
- Bar plots not ideal for small value differences
- Histogram limitations for uncorrelated variables
- Pie charts avoided for more than 5-7 categories
- Color palette selection critical for accessibility

### Statistical Considerations
- Correlation does not imply causation
- Sample size varies across seasons
- Outlier impact on aggregate statistics
- Position-based performance variations

---

## Contributing

We welcome contributions! Areas for improvement:

- Additional player comparisons
- New visualization types
- Performance optimizations
- Documentation enhancements
- Bug fixes and testing

Please submit pull requests with clear descriptions of changes.

---

## License

This project is for educational and research purposes. NBA statistics are property of the National Basketball Association. Use of nba_api is subject to their terms of service.

---

## Acknowledgments

- **NBA.com** for providing comprehensive statistics
- **nba_api community** for the excellent Python package
- Basketball analytics community for inspiration and best practices

---

## References

1. [nba_api GitHub Repository](https://github.com/swar/nba_api)
2. [NBA Official Statistics](https://www.nba.com/stats)
3. [NBA Court Drawing Guide](https://gist.github.com/giasemidis/2e271f98567b94f634b3b628921cc0bd)
4. [National Basketball Association - Wikipedia](https://en.wikipedia.org/wiki/National_Basketball_Association)
5. [NBA Savant - Advanced Statistics](https://www.nbasavant.com/)
6. [NBA Visualization Examples - Towards Data Science](https://towardsdatascience.com/10-unique-visualizations-of-the-nba-b981cfdb78bf)

---

## Version History

- **v1.0** (Initial Release): Core visualizations for 4 players
- **Future:** Real-time analysis, additional sports, ML integration

---

*This project demonstrates the power of data visualization in sports analytics, providing actionable insights for team management, player development, and strategic decision-making.*
