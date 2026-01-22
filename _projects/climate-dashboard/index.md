# Visualisasi Korelasi dengan Plotly Express
fig3_scatter = px.scatter(
    filtered_merged.dropna(subset=['CO2 Emissions (Mt CO2e)']),
    x='Renewable Capacity (W/capita)',
    y='CO2 Emissions (Mt CO2e)',
    color='Country',
    hover_data=['Year'],
    title='Renewable Capacity vs CO2 Emissions',
    labels={
        'Renewable Capacity (W/capita)': 'Kapasitas Terbarukan (W/kapita)',
        'CO2 Emissions (Mt CO2e)': 'Emisi CO2 (Mt)'
    }
)
fig3_scatter.update_layout(transition={'duration': 500, 'easing': 'cubic-in-out'})
st.plotly_chart(fig3_scatter, use_container_width=True)