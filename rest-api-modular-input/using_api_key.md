
# Overview

This documentation guides users through the process of integrating OpenWeatherMap's Current Weather Data API with Splunk, using a REST API Modular Input App. The integration involves obtaining an API key, configuring a new index in Splunk, and setting up the REST API Modular Input App with the obtained key. Additionally, it provides steps to validate the data in Splunk and create a sample dashboard to visualize OpenWeather data.

# API Key Authentication

![api_key_authentication](https://github.com/learncytech4good/youtube_tutorials/assets/156148981/7b78b31b-fb60-45e6-9b3d-aaaf08cadf17)

## 1. Obtaining OpenWeatherMap API Key for Current Weather Data

Follow these steps to obtain an API key for accessing OpenWeatherMap's Current Weather Data API.

1. Create an OpenWeatherMap Account

Go to the [OpenWeatherMap website](https://openweathermap.org/) and click on the "Sign Up" button. Fill in the required information to create a new account.

2. Login to Your OpenWeatherMap Account

After creating your account, log in to the OpenWeatherMap website using your credentials.

3. Navigate to API Keys Page

Once logged in, go to the "API keys" section. You can find this in the top navigation bar or in your account settings.

4. Generate a New API Key

Click on the "Generate" button or a similar option to create a new API key.

5. Choose the API Plan

Select the plan that fits your needs. For Current Weather Data, the Free plan may be sufficient.

6. Complete the Process

Follow the instructions provided to complete the API key generation process. This may involve confirming your email address or agreeing to terms and conditions.

7. Retrieve Your API Key

Once the process is complete, you will be provided with an API key. This key is essential for making API requests to OpenWeatherMap's Current Weather Data API.

8. Securely Store Your API Key

Copy the generated API key and securely store it. Do not share your API key publicly or expose it in client-side code, as it could be misused.

## 2. Create a New Index in Splunk Web

Follow these steps to create a new index named "weather" using Splunk Web:

1. **Access Splunk Web:**
   Open your web browser and navigate to the Splunk Web interface. Typically, this is done by entering the URL `http://localhost:8000` in the address bar.

2. **Login:**
   Log in to Splunk with your credentials. Ensure that you have the necessary permissions to create indexes.

3. **Navigate to Settings:**
   Once logged in, click on the gear icon in the top right corner of the Splunk Web interface to access the "Settings" menu.

4. **Select Indexes:**
   In the "Settings" menu, find and click on the "Indexes" option. This will take you to the "Indexes" page where you can manage existing indexes and create new ones.

5. **Create New Index:**
   On the "Indexes" page, look for the "New Index" button and click on it to initiate the index creation process.

6. **Provide Index Details:**
   - **Index Name:** Enter "weather" as the name for the new index.
   - **Index ID:** Splunk will automatically generate an ID for the index.
   - **Cold Path:** Specify the location for storing cold data.
   - **Thawed Path:** Specify the location for thawed data.
   - **Home Path:** Specify the location for storing hot and warm data.

7. **Review and Save:**
   Review the index details to ensure accuracy. Double-check the paths and other settings. If everything looks correct, click the "Save" or "Submit" button to create the new "weather" index.

8. **Verify Creation:**
   After saving, go back to the "Indexes" page and confirm that the "weather" index is now listed. You should see it along with other existing indexes.

## 3. Obtaining a 14-Day Free Trial Activation Key for BaboonBones Rest API Modular Input App

Follow these steps to obtain a free 14-day trial activation key for the BaboonBones Rest API Modular Input App:

1. Visit the official BaboonBones website at [https://www.baboonbones.com/#activation](https://www.baboonbones.com/#activation).

2. Complete the necessary information on the activation form. Ensure that you select the "Rest API Modular Input" as the app of interest.

3. Click on the "Get Free 14-Day Trial Key" button to submit your request.

4. Check your email for the activation key. BaboonBones will send the key to the email address provided during the registration process.

## 4. Configure REST API Modular Input using API Key Authentication

1. **REST API Input Name:**
   - Set the name for the REST API input. In this example, use `weather_api`.

2. **Activation Key:**
   - Insert the activation key sent to your email.

3. **Endpoint URL:**
   - Insert the API endpoint URL for the OpenWeather API along with the API Key. For example:
     ```
     https://api.openweathermap.org/data/2.5/weather?q={CITY_NAME}&appid={API_KEY}
     ```
     Replace `{CITY_NAME}` with the desired city name and `{API_KEY}` with your actual OpenWeather API key.

4. **Authentication Type:**
   - Set the Authentication Type to `basic`.

5. **Polling Interval:**
   - Enter a number in seconds depending on your needs. This determines how often the app fetches data from the specified API.

6. **Sourcetype:**
   - Set the Sourcetype to `weather_api`.

7. **Index:**
   - Set the Index to `weather`.

## 5. Validate OpenWeather API Data in Splunk

1. **Log in to Splunk:**
   - Open your Splunk instance in a web browser.
   - Log in with your credentials.

2. **Access the Search & Reporting App:**
   - Navigate to the "Search & Reporting" app.

3. **Run the Search Query:**
   - In the search bar, input the following query:
     ```spl
     index="weather"
     ```
   - Press Enter to execute the query.

4. **Validate Results:**
   - Ensure that the search returns OpenWeather API data for the specified index ("weather").
   - Examine the data fields and verify that it matches the expected OpenWeather API data.

## 6. Create a Sample Dashboard using OpenWeather API Data

1. **Access the Dashboard Creation Interface:**
   - Navigate to the "Dashboards" app in Splunk.

2. **Create a New Dashboard:**
   - Create a new dashboard or open an existing one where you want to add the OpenWeather information.

3. **Insert Time Picker Input:**
   - Copy and paste the provided form code into your dashboard XML.

4. **Temperature Now Panel:**
   - Add a single value panel for the current temperature.
   - Configure the search query to fetch and display the latest temperature from the OpenWeather API.

5. **Feels Like Panel:**
   - Add another single value panel for the "Feels Like" temperature.
   - Configure the search query to fetch and display the latest "Feels Like" temperature from the OpenWeather API.

6. **Temperature Overtime Chart:**
   - Add a chart panel to display temperature trends over time.
   - Configure the search query to fetch and display time-charted data for both current temperature and "Feels Like" temperature.

7. **Configure Chart Options:**
   - Adjust chart options and settings based on your preferences, as outlined in the provided XML code.

8. **Save and View Dashboard:**
   - Save the dashboard and view it to ensure that it displays the OpenWeather data correctly.

9. **Test Time Picker:**
   - Test the time picker functionality to verify that the dashboard updates dynamically based on the selected time range.

10. **Final Validation:**
   - Verify that the dashboard provides accurate and real-time information from the OpenWeather API.

Copy of XML Code for Dashboard

```xml
<form version="1.1" theme="dark">
  <label>OpenWeather Toronto</label>
  <fieldset submitButton="false">
    <input type="time" token="timepicker" searchWhenChanged="true">
      <label></label>
      <default>
        <earliest>0</earliest>
        <latest></latest>
      </default>
    </input>
  </fieldset>
  <row>
    <panel>
      <single>
        <search>
          <query>index=weather sourcetype=weather_api
| stats latest(main.temp) AS temp_now
| eval temp_now = round(temp_now)</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="drilldown">none</option>
        <option name="rangeColors">["0x53a051","0x0877a6","0xf8be34","0xf1813f","0xdc4e41"]</option>
        <option name="refresh.display">progressbar</option>
        <option name="underLabel">Temperature Now</option>
        <option name="unit">°C</option>
      </single>
    </panel>
    <panel>
      <single>
        <search>
          <query>index=weather sourcetype=weather_api
| stats latest(main.feels_like) AS feels_like
| eval feels_like = round(feels_like)</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="drilldown">none</option>
        <option name="rangeColors">["0x53a051","0x0877a6","0xf8be34","0xf1813f","0xdc4e41"]</option>
        <option name="refresh.display">progressbar</option>
        <option name="underLabel">Feels Like</option>
        <option name="unit">°C</option>
      </single>
    </panel>
  </row>
  <row>
    <panel>
      <title>Temperature Overtime</title>
      <chart>
        <search>
          <query>index=weather sourcetype=weather_api
| timechart latest(main.temp) AS temp_now latest(main.feels_like) as feels_like span=5m
| eval temp_now = round(temp_now), feels_like = round(feels_like)</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="charting.axisLabelsX.majorLabelStyle.overflowMode">ellipsisNone</option>
        <option name="charting.axisLabelsX.majorLabelStyle.rotation">0</option>
        <option name="charting.axisTitleX.visibility">visible</option>
        <option name="charting.axisTitleY.visibility">visible</option>
        <option name="charting.axisTitleY2.visibility">visible</option>
        <option name="charting.axisX.abbreviation">none</option>
        <option name="charting.axisX.scale">linear</option>
        <option name="charting.axisY.abbreviation">none</option>
        <option name="charting.axisY.scale">linear</option>
        <option name="charting.axisY2.abbreviation">none</option>
        <option name="charting.axisY2.enabled">0</option>
        <option name="charting.axisY2.scale">inherit</option>
        <option name="charting.chart">column</option>
        <option name="charting.chart.bubbleMaximumSize">50</option>
        <option name="charting.chart.bubbleMinimumSize">10</option>
        <option name="charting.chart.bubbleSizeBy">area</option>
        <option name="charting.chart.nullValueMode">gaps</option>
        <option name="charting.chart.overlayFields">feels_like</option>
        <option name="charting.chart.showDataLabels">none</option>
        <option name="charting.chart.sliceCollapsingThreshold">0.01</option>
        <option name="charting.chart.stackMode">default</option>
        <option name="charting.chart.style">shiny</option>
        <option name="charting.drilldown">none</option>
        <option name="charting.layout.splitSeries">0</option>
        <option name="charting.layout.splitSeries.allowIndependentYRanges">0</option>
        <option name="charting.legend.labelStyle.overflowMode">ellipsisMiddle</option>
        <option name="charting.legend.mode">standard</option>
        <option name="charting.legend.placement">right</option>
        <option name="charting.lineWidth">2</option>
        <option name="refresh.display">progressbar</option>
        <option name="trellis.enabled">0</option>
        <option name="trellis.scales.shared">1</option>
        <option name="trellis.size">medium</option>
      </chart>
    </panel>
  </row>
</form>
```

## Conclusion

With these steps, you should have a functioning Splunk dashboard that displays OpenWeather API data and allows dynamic time filtering. Adjustments can be made based on specific customization needs and preferences.
