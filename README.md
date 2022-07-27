# Cluster-chart-in-R.-programming-

# Load pacman, rio and tidyverse
pacman::p_load(pacman, rio, tidyverse)

### loading the data, making psychRegions as factor and renaming it as y

data <- import("StateData.xlsx") %>% as_tibble() %>% 
         select(state_code, psychRegions, instagram:modernDance) %>%
         mutate(psychRegions = as.factor(psychRegions)) %>%
         rename(y = psychRegions) %>% print()

view(data)

#Calculating the clusters 
hierachical_cluster <- data %>%  # Getting the data 
                     dist %>%   # computing the distance or dissimilarity matrix
                     hclust     # computing the hierarchical cluster

### Plotting the Dendrogram 
hierachical_cluster %>% plot(labels = data$state_code)

### Visualizing the subdivisions

hierachical_cluster %>% rect.hclust(k = 4, border = "green") # 4 boxes 
hierachical_cluster %>% rect.hclust(k = 2, border = "red") # 2 boxes 
hierachical_cluster %>% rect.hclust(k = 8, border = "blue") # 8 boxes 



