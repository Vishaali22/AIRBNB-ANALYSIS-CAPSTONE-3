# AIRBNB-ANALYSIS-CAPSTONE-3
AIRBNB ANALYSIS CAPSTONE 3
Streamlit Airbnb Analysis Project
This project is a Streamlit application that provides an interactive interface for analyzing Airbnb data. The application allows users to explore and visualize data related to Airbnb listings, including neighborhood groups, room types, prices, and more. Below is a detailed breakdown of the code and its functionality.

Libraries and Configurations
Import Libraries:

streamlit for creating the web app interface.
streamlit_option_menu for creating a navigation menu.
plotly.express and matplotlib.pyplot for creating visualizations.
pandas for data manipulation.
os for interacting with the operating system.
PIL.Image for handling images.
warnings to filter out warnings.
Set Page Configuration:

python
Copy code
st.set_page_config(page_title="AirBnb-Analysis by VISHAALI RJ!!!", page_icon=":bar_chart:", layout="wide")
Page Title and Custom Styles:

python
Copy code
st.title(":bar_chart:   AirBnb-Analysis")
st.markdown('<style>div.block-container{padding-top:1rem;}</style>', unsafe_allow_html=True)
Navigation Menu
The application uses a horizontal navigation menu with three options: Home, Explore Data, and Contact.

python
Copy code
SELECT = option_menu(
    menu_title=None,
    options=["Home", "Explore Data", "Contact"],
    icons=["house", "bar-chart", "phone"],
    default_index=2,
    orientation="horizontal",
    styles={"container": {"padding": "0!important", "background-color": "white", "size": "cover", "width": "100"},
            "icon": {"color": "black", "font-size": "20px"},
            "nav-link": {"font-size": "20px", "text-align": "center", "margin": "-2px", "--hover-color": "#6F36AD"},
            "nav-link-selected": {"background-color": "#6F36AD"}}
)
Home Section
Displays an introduction to Airbnb, its background, and the skills and domain knowledge acquired from this project.

python
Copy code
if SELECT == "Home":
    st.header('Airbnb Analysis')
    st.subheader("Airbnb is an American San Francisco-based company operating an online marketplace for short- and long-term homestays and experiences...")
    st.image(Image.open(r"C:\Users\Vishaali Naagaarjun\OneDrive\Desktop\CAPSTONE 3\airbnb image.jpeg"), use_column_width=True)
Explore Data Section
Allows users to upload a dataset, apply filters, and visualize the data.

File Upload:

python
Copy code
fl = st.file_uploader(":file_folder: Upload a file", type=(["csv", "txt", "xlsx", "xls"]))
if fl is not None:
    filename = fl.name
    st.write(filename)
    df = pd.read_csv(filename, encoding="ISO-8859-1")
else:
    os.chdir(r"C:\Users\Vishaali Naagaarjun\OneDrive\Desktop\CAPSTONE 3")
    df = pd.read_csv("Airbnb NYC 2019.csv", encoding="ISO-8859-1")
Filters and Data Selection:

python
Copy code
st.sidebar.header("Choose your filter: ")
neighbourhood_group = st.sidebar.multiselect("Pick your neighbourhood_group", df["neighbourhood_group"].unique())
neighbourhood = st.sidebar.multiselect("Pick the neighbourhood", df2["neighbourhood"].unique())
Visualizations:

Bar chart for room types and their prices.
Pie chart for neighborhood groups and their prices.
Scatter plot for room types in neighborhoods.
python
Copy code
fig = px.bar(room_type_df, x="room_type", y="price", text=['${:,.2f}'.format(x) for x in room_type_df["price"]], template="seaborn")
st.plotly_chart(fig, use_container_width=True, height=200)

fig = px.pie(filtered_df, values="price", names="neighbourhood_group", hole=0.5)
fig.update_traces(text=filtered_df["neighbourhood_group"], textposition="outside")
st.plotly_chart(fig, use_container_width=True)

data1 = px.scatter(filtered_df, x="neighbourhood_group", y="neighbourhood", color="room_type")
data1['layout'].update(title="Room_type in the Neighbourhood and Neighbourhood_Group wise data using Scatter Plot.")
st.plotly_chart(data1, use_container_width=True)
Data Table and Download Options:

python
Copy code
with st.expander("room_type wise price"):
    st.write(room_type_df.style.background_gradient(cmap="Blues"))
    csv = room_type_df.to_csv(index=False).encode('utf-8')
    st.download_button("Download Data", data=csv, file_name='Airbnb NYC 2019.csv', mime="text/csv")

with st.expander("neighbourhood_group wise price"):
    neighbourhood_group = filtered_df.groupby(by="neighbourhood_group", as_index=False)["price"].sum()
    st.write(neighbourhood_group.style.background_gradient(cmap="Oranges"))
    csv = neighbourhood_group.to_csv(index=False).encode('utf-8')
    st.download_button("Download Data", data=csv, file_name="neighbourhood_group.csv", mime="text/csv")
Map View:

python
Copy code
st.subheader("Airbnb Analysis in Map view")
df = df.rename(columns={"Latitude": "lat", "Longitude": "lon"})
st.map(df)
Contact Section
Displays the author's contact information and social media links.

python
Copy code
if SELECT == "Contact":
    Name = (f'{"Name :"}  {"VISHAALI RJ"}')
    mail = (f'{"Mail :"}  {"vyshjuuu22@gmail.com"}')
    description = "An upcoming DATA-SCIENTIST..!"
    social_media = {
        "Youtube": "https://www.youtube.com/@sarabistales-vyshjuuu",
        "GITHUB": "https://github.com/Vishaali22",
        "LINKEDIN": "https://www.linkedin.com/in/vyshali-rj-4463b2227",
        "Instagram": "https://www.instagram.com/vi_sha_ali/",
    }
    col1, col2 = st.columns(2, gap="large")
    col1.image(Image.open(r"C:\Users\Vishaali Naagaarjun\OneDrive\Desktop\CAPSTONE 3\AIRBNB1.jpeg"), width=300)
    col2.subheader(Name)
    col2.subheader(mail)
    col2.subheader(description)
    for index, (platform, link) in enumerate(social_media.items()):
        col2.write(f"[{platform}]({link})")
Project Skills and Technologies
Python Scripting: For data manipulation and analysis.
Data Preprocessing: Cleaning and preparing data for analysis.
Visualization: Creating charts and plots using Plotly and Matplotlib.
Exploratory Data Analysis (EDA): Analyzing data to uncover patterns and insights.
Streamlit: Building an interactive web application.
PowerBI: (Optional) For creating advanced visualizations and dashboards.
Domains
Travel Industry
Property Management
Tourism
Conclusion
This Streamlit application is a comprehensive tool for analyzing Airbnb data. It allows users to upload datasets, apply filters, and visualize data through various charts and maps. The project showcases essential skills in data analysis, visualization, and web app development, making it a valuable addition to the portfolio.
