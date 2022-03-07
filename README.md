# surfs_up
Mod 9 - Advanced Data Storage and Retrieval 

# Overview 
W. Avy is requesting more information about temperature trends before opening the surf shop. Specifically, he wants temperature data for the months of June and December in Oahu, in order to determine if the surf and ice cream shop business is sustainable year-round.
## Results: There is a bulleted list that addresses the three key differences in weather between June and December. (6 pt)
1.	Average temperature in June is ~75 degrees vs ~71 degrees in December.
2.	There is a wider range in temperatures for December vs June. 
a.	June min/max = 64/85, or a range of 21 degrees. 
b.	December min/max = 56/83, or a range of 27 degrees.
 
 ![June_Dec Temps](https://user-images.githubusercontent.com/96449605/156910429-16aee879-1f43-4afb-ba3c-aba834abd200.png)

3.	The December histogram graph has a more symmetrical, unimodal distribution compared to the June graph that is more multimodal, having more than one peak in temperatures across the month.
   
  ![June](https://user-images.githubusercontent.com/96449605/156910443-99779294-268d-4b2d-96db-e104690d5b00.png)

  ![December](https://user-images.githubusercontent.com/96449605/156910450-77ac9417-7e72-44cc-9d5a-516d2e409ce3.png)

### Summary: There is a high-level summary of the results and there are two additional queries to perform to gather more weather data for June and December. (5 pt)
	The initial goal was to do a weather analysis as due diligence for fully investing in a Surf ‘N’ Shake Shop in Hawaii. From the initial analysis, the weather is favorable: the temperatures are generally warm year-round and the precipitation is marginal to the point where it shouldn’t have a major impact on revenue.
2 Additional Queries for June and December weather data:
# Additional Query 1: June Precipitation
june_temp_prcp = session.query(Measurement.tobs,Measurement.prcp).filter(extract('month', Measurement.date) == 6).all()
june_temp_prcp_df = pd.DataFrame(june_temp_prcp)
# print(june_temp_prcp_df)
june_temp_prcp_df.describe()

 ![Query 1A](https://user-images.githubusercontent.com/96449605/156910462-f1f1da46-b49b-4c97-9053-d890649e58f7.png)

June graph of temp x prcp with trendline
june_temp_prcp_df = pd.DataFrame(june_temp_prcp, columns=['tobs','prcp'])
have to drop Nans to plot on the scatterplot
june_temp_prcp_df = june_temp_prcp_df.dropna()
june_temp_prcp_df.plot.scatter('tobs', 'prcp')
plt.tight_layout()
plt.title('June Temperature by Precipitation')
plt.xlim([55, 85])
plt.ylim([0,8])

Add Trendline and equation
slope, intercept, r_value, p_value, std_err = stats.linregress(june_temp_prcp_df['tobs'],june_temp_prcp_df['prcp'])
sns.regplot(x='tobs', y='prcp', data=june_temp_prcp_df, ci=None, label="y={0:.4f}x+{1:.4f}".format(slope,intercept)).legend(loc="best")

 ![Query 1B](https://user-images.githubusercontent.com/96449605/156910470-50af236f-e058-48dd-a66a-65671b8269fa.png)

Additional Query 2: December Precipitation 
dec_temp_prcp = session.query(Measurement.tobs,Measurement.prcp).filter(extract('month', Measurement.date) == 12).all()
dec_temp_prcp_df = pd.DataFrame(dec_temp_prcp)
print(dec_temp_prcp_df)
dec_temp_prcp_df.describe()

 ![Query 2A](https://user-images.githubusercontent.com/96449605/156910484-6123d89d-0c0e-4c4d-a296-0c0de9e65bb4.png)

Dec graph of temp x prcp with trendline
dec_temp_prcp_df = pd.DataFrame(dec_temp_prcp, columns=['tobs','prcp'])
have to drop Nans to plot on the scatterplot
dec_temp_prcp_df = dec_temp_prcp_df.dropna()
dec_temp_prcp_df.plot.scatter('tobs', 'prcp')
plt.tight_layout()
plt.title('December Temperature by Precipitation')
plt.xlim([55, 85])
plt.ylim([0,8])

Add Trendline and equation
slope, intercept, r_value, p_value, std_err = stats.linregress(dec_temp_prcp_df['tobs'], dec_temp_prcp_df['prcp'])
sns.regplot(x='tobs', y='prcp', data=dec_temp_prcp_df, ci=None, label="y={0:.4f}x+{1:.4f}".format(slope,intercept)).legend(loc="best")
 
![Query 2B](https://user-images.githubusercontent.com/96449605/156910490-ad59db3a-86da-4cf3-8cf6-1f4e20a8dfb9.png)
