# similar-water-regions
In this project we look at the global surface water explorer and find tiles of areas that are similar to each other in the entire world using the European Commision Global Surface satellite water dataset, based on their area of water that are either unchanged, lost or found new areas of permanent water sources.

Since the dataset is quite large(~ 8gb of Tiff files), we used spark for a distributed way to solve the problem. Each tile was spanned a region of 10 degree in latitude and 10 degree in longitude (40,000x40,000 pixels). So we used PIL library and spark in python to divide the large tiff files into smaller tiles of 2000x2000 pixels size (spanning across 0.5 degree latitude and 0.5 degree longitude), encompassing approx. area of 100 sq. km.  

Within each tile, we counted the area of surface water lost permanently within each tile, surface water new found and area of water that remained unchanged. We used this data to create for each tile, a feature = (unchanged water area, lost water bodies, new found water bodies). We saved these into disks as text files for smaller dataset.  

Using these feature vector, we performed a k means clustering. Using elbow analysis, we found a k of size 10. Given any coordinates, it could easily tell the coordinates that have similar water trends using nearest neighbor search.  

We used pyspark, jupyter notebook and numpy to do this analysis. Our final results are the top 10 regions with coordinates that show similar trends in surface water loss/water inundated regions.


References:

Dataset:
Jean-Francois Pekel, Andrew Cottam, Noel Gorelick, Alan S. Belward, High-resolution mapping of global surface water and its long-term changes. Nature 540, 418-422 (2016). (doi:10.1038/nature20584)
