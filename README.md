# SQL Analysis for COVID Database

## Overview

This project focuses on analyzing COVID-19 data using SQL. The database includes comprehensive information about COVID-19 cases, vaccinations, and testing statistics globally, allowing for data-driven insights into the pandemic's progression and impact.



## Key Features

- **Data Structure:**
  - A structured database with tables for:
    - **`Cases`**: Tracks confirmed cases, recoveries, and deaths by country and date.
    - **`Vaccinations`**: Logs vaccination doses administered and population coverage.
    - **`Testing`**: Includes testing rates and positivity percentages.
  - Relationships between tables for integrated analysis.

- **SQL Queries for Analysis:**
  - Total and active case trends by country.
  - Vaccination progress, including percentage of the population vaccinated.
  - Mortality and recovery rates.
  - Positivity rates and their relationship with testing levels.
  - Identification of COVID-19 peaks by region.

- **Visualizations:**
  - Results are designed for easy integration with BI tools (e.g., Tableau, Power BI) for dashboards.



## Getting Started

### Prerequisites

- **Database Engine:** MySQL, PostgreSQL, or any SQL-compatible database.
- **SQL Client:** Workbench, DBeaver, or a similar tool.
- **Dataset:** Downloaded COVID-19 dataset in CSV format from a reputable source such as [Our World in Data](https://ourworldindata.org/coronavirus-data).

### Setup Instructions

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/SQL-Analysis-COVID.git
   cd SQL-Analysis-COVID
   ```

2. **Import Dataset into the Database:**
   - Use provided scripts in the `Data/` directory to create tables and import data.

3. **Run SQL Queries:**
   - Open the `SQL Queries/` folder and execute the desired `.sql` files for analysis.

4. **Optional: Integrate with BI Tools:**
   - Export query results for visualization or connect your database directly to a BI tool.



## File Structure

```plaintext
SQL-Analysis-COVID/
├── Data/
│   ├── create_tables.sql  # SQL script for table creation.
│   ├── import_data.sql    # Script to load COVID datasets.
├── SQL Queries/
│   ├── case_analysis.sql  # Analysis of COVID case trends.
│   ├── vaccination.sql    # Queries for vaccination progress.
│   ├── testing.sql        # Insights into testing and positivity rates.
└── README.md              # Project overview and instructions.
```



## Sample Queries

### Example 1:  Total Population vs Vaccinations
```sql
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, SUM(CONVERT(int,vac.new_vaccinations)) OVER (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
From PortfolioProject..CovidDeaths dea
Join PortfolioProject..CovidVaccinations vac
	On dea.location = vac.location
	and dea.date = vac.date
where dea.continent is not null 
order by 2,3
```

### Example 2: Creating View to store data for later visualizations
```sql
Create View PercentPopulationVaccinated as
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, SUM(CONVERT(int,vac.new_vaccinations)) OVER (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
From PortfolioProject..CovidDeaths dea
Join PortfolioProject..CovidVaccinations vac
	On dea.location = vac.location
	and dea.date = vac.date
where dea.continent is not null 
```

### Example 3: Showing contintents with the highest death count per population
```sql
Select continent, MAX(cast(Total_deaths as int)) as TotalDeathCount
From PortfolioProject..CovidDeaths
Where continent is not null 
Group by continent
order by TotalDeathCount desc
```



## License

This project is licensed under the MIT License.


## Contact

For questions or collaboration:
- **Email:** kiroemad239@gmail.com
- **GitHub:** [Kirolos00Daniel](https://github.com/your-username)

