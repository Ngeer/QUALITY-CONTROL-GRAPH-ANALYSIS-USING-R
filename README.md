# QUALITY-CONTROL-GRAPH-ANALYSIS-USING-R
How to use R for creation of quality control charts
#Read your CSV file
# Replace "yourfile.csv" with the actual filename/path
df <- read.csv("Fecal Coliform.csv")

# 2. Convert Round column to factor to preserve order on x-axis
df$Round <- factor(df$Round, levels = df$Round)

# 3. Convert table from wide format → long format
df_long <- pivot_longer(
  df,
  cols = -Round,
  names_to = "variable",
  values_to = "value"
)

 stuart <- ggplot(df_long, aes(x = Round, y = value, color = variable, group = variable)) +
  geom_line(linewidth = 1.2) +
  geom_point(size = 2) +
  labs(title = "Fecal Coliform Control Chart", x = "Analyst", y = "Z score") +
  scale_y_continuous(
    limits = c(-3, 3),
    breaks = c(-3, -2, -1, 0, 1, 2, 3)
  ) +
  theme_minimal() +
  theme(
  plot.title = element_text(face = 'bold', ,hjust = 0.5),
  axis.text.x = element_text( angle = 45,hjust = 0.5)
  )

 png('stuart.png')

