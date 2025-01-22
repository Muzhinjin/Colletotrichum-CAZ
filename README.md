# Colletotrichum-CAZ

# Load necessary libraries
library(ggplot2)
library(extrafont)

# Create the data frame
data <- data.frame(
  CAZyme = c("AA", "CBM", "CE", "GH", "GT", "PL"),
  `6Ca` = c(196, 9, 70, 379, 103, 43),
  `34Ca` = c(198, 9, 73, 378, 101, 42),
  `40Ca` = c(166, 9, 66, 368, 102, 42),
  `28Cg` = c(178, 13, 60, 404, 102, 46),
  `57Cg` = c(187, 12, 57, 410, 102, 47),
  `58cg` = c(185, 12, 63, 413, 105, 47),
  `84Cg` = c(202, 15, 64, 413, 110, 47)
)

# Reshape the data for ggplot (from wide to long format)
library(reshape2)
data_melted <- melt(data, id.vars = "CAZyme")


# Create the plot
ggplot(data_melted, aes(x = variable, y = value, fill = CAZyme)) +
  geom_bar(stat = "identity") +
  scale_fill_manual(values = c("lightgreen", "lightcoral", "cyan", "red", "gray", "orange")) + # Muted colors
  theme_minimal() +
  labs(title = NULL,  # Remove overall title
       x = expression(italic("Colletotrichum") ~ "isolates"),  # Italicize Colletotrichum
       y = "CAZymes number",
       fill = NULL) +  # Remove legend title
  scale_x_discrete(labels = function(x) gsub("^X", "", x)) +  # Remove 'X' prefix from x labels
  theme(
    text = element_text(family = "Times New Roman", size = 12), # General text
    axis.title.x = element_text(family = "Times New Roman", size = 12),  # X-axis label
    axis.title.y = element_text(family = "Times New Roman", size = 12),  # Y-axis label
    axis.text.x = element_text(family = "Times New Roman", size = 12),    # X-axis text (isolate names)
    axis.text.y = element_text(family = "Times New Roman", size = 12),    # Y-axis text (numbers)
    legend.title = element_blank()  # Remove legend title
  )
# Save the plot as a PNG file
ggsave("cazymes_plot.png", plot = plot, width = 360 / 72, height = 360 / 72, units = "in")  # 72 dpi



