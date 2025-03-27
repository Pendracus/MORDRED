# Vensim Code MORDRED-1.1
Growth_slowdown_factor_climate_damages_in_labor_intensity=
	MAX(0,MIN(1, 2*Growth_slowdown_labour_damage_factor-2))
	~	
	~	MAX(0,MIN(1, 2*Growth_slowdown_labour_factor-2))
	|

Damages_on_labour_productivity_isengard=
	Damages_on_labour_productivity_produced_by_heat[isengard]
	~	
	~		|

Growth_slowdown_labour_damage_factor=
	MIN(2,MAX(1,2.5-((0.5/0.3)*added_climate_damage_on_labor_intensity_isengard)))
	~	
	~		|

added_climate_damage_on_labor_intensity_isengard=
	Damages_on_labour_productivity_isengard+output_losses_due_to_climate_change_isengard
	~	
	~		|

Growth_slowdown_factor=
	if_then_else(SWITCH_GROWTH_SLOWDOWN_SP=0,1,
	MAX(0,
	MIN(1, (20*Growth_slowdown-20)*Growth_slowdown_factor_climate_damages_in_labor_intensity\
		)
	)
	)
	~	
	~		|

output_losses_due_to_climate_change_isengard=
	Output_losses_due_to_climate_change[isengard]
	~	
	~		|

land_shares_in_total_land[LAND]=
	Land_distribution[LAND]/Disposable_land
	~	
	~		|

Maximum_population_in_subsistence=
	Land_distribution[food_land_subsistence]/Subsistence_land_intensity
	~	
	~	Land_distribution[food land subsistence]/INITIAL_SUBSISTENCE_LAND_INTENSITY
	|

consumption_per_capita_to_accumulate[REGION, CLASS]=
	Consumption_per_capita[REGION,CLASS]
	~	
	~		|

cumulative_consumption[CONSUMPTION_DEMAND]= INTEG (
	consumption_to_accumulate[CONSUMPTION_DEMAND],
		0)
	~	
	~		|

average_consumption_per_capita_formal_economy=
	((0.2*Total_population_in_formal_economy_by_region[Centre]*Consumption_per_capita[Centre\
		,high]+0.5*Total_population_in_formal_economy_by_region[Centre]*Consumption_per_capita\
		[Centre,medium]+0.3*Total_population_in_formal_economy_by_region[Centre]*Consumption_per_capita\
		[Centre,low])+
	(0.2*Total_population_in_formal_economy_by_region[Semiperiphery]*Consumption_per_capita\
		[Semiperiphery,high]+0.5*Total_population_in_formal_economy_by_region[Semiperiphery\
		]*Consumption_per_capita[Semiperiphery,medium]+0.3*Total_population_in_formal_economy_by_region\
		[Semiperiphery]*Consumption_per_capita[Semiperiphery,low])+
	(0.2*Total_population_in_formal_economy_by_region[Periphery]*Consumption_per_capita[\
		Periphery,high]+0.5*Total_population_in_formal_economy_by_region[Periphery]*Consumption_per_capita\
		[Periphery,medium]+0.3*Total_population_in_formal_economy_by_region[Periphery]*Consumption_per_capita\
		[Periphery,low]))/Total_population_in_formal_economy
	~	
	~		|

average_consumption_per_capita_formal_economy_by_region[REGION]=
	(0.2*Total_population_in_formal_economy_by_region[REGION]*Consumption_per_capita[REGION\
		,high]+0.5*Total_population_in_formal_economy_by_region[REGION]*Consumption_per_capita\
		[REGION,medium]+0.3*Total_population_in_formal_economy_by_region[REGION]*Consumption_per_capita\
		[REGION,low])
	~	
	~		|

consumption_to_accumulate[CONSUMPTION_DEMAND]=
	Final_demand_by_components[CONSUMPTION_DEMAND]
	~	
	~		|

cumulative_per_capita_consumption[REGION,CLASS]= INTEG (
	consumption_per_capita_to_accumulate[REGION,CLASS],
		0)
	~	
	~		|

ratio_high_C_to_low_C=
	ZIDZ(Consumption_per_capita[Centre,high], Consumption_per_capita[Centre,low])
	~	
	~		|

ratio_high_C_to_high_S=
	ZIDZ(Consumption_per_capita[Centre,high], Consumption_per_capita[Semiperiphery,high]\
		)
	~	
	~		|

ratio_high_S_to_high_P=
	ZIDZ(Consumption_per_capita[Semiperiphery,high], Consumption_per_capita[Periphery,high\
		])
	~	
	~		|

Total_population_by_region[REGION]=
	Total_population_in_formal_economy_by_region[REGION]+Total_population_in_subsistence_by_region\
		[REGION]
	~	
	~		|

ratio_high_S_to_low_S=
	ZIDZ(Consumption_per_capita[Semiperiphery,high], Consumption_per_capita[Semiperiphery\
		,low])
	~	
	~		|

ratio_high_P_to_low_P=
	ZIDZ(Consumption_per_capita[Periphery,high], Consumption_per_capita[Periphery,low])
	~	
	~		|

ratio_high_C_to_low_P=
	ZIDZ(Consumption_per_capita[Centre,high], Consumption_per_capita[Periphery,low])
	~	
	~		|

Total_emissions_GtCO2e_with_LUC=
	(Total_anthropogenic_CO2_emissions/1000)+Total_anthropogenic_non_CO2_emissions_in_CO2_equivalents
	~	GTCO2e/Year
	~		|

share_LUC_in_CO2emissions=
	ZIDZ(Anthropogenic_LUC_CO2_Emissions,Total_anthropogenic_CO2_emissions)
	~	MtCO2/Year
	~		|

Share_of_each_sector_in_gfcf[SECTORS]=
	INITIAL_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION
	[SECTORS]+RAMP(ZIDZ(TARGET_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION_SP[SECTORS\
		]-INITIAL_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION
	[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100)
	~	1
	~		|

Share_of_each_sector_in_government_consumption[SECTORS]=
	INITIAL_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION[SECTORS]+RAMP(ZIDZ(TARGET_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION_SP\
		[SECTORS]-INITIAL_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION[SECTORS],2100-INITIAL_TIME\
		), INITIAL_TIME , 2100)
	~	
	~		|

TARGET_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TARGET_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION_SP'\
		)
	~	
	~		|

Desired_government_consumption_by_sector_and_region[REGION,SECTORS]=
	Desired_government_consumption_by_region[REGION]*Share_of_each_sector_in_government_consumption\
		[SECTORS]
	~	million_euro/Year
	~		|

TARGET_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TARGET_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION'\
		)
	~	
	~		|

INITIAL_SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'SHARE_OF_EACH_SECTOR_IN_GOVERNMENT_CONSUMPTION'\
		)
	~	
	~		|

INITIAL_SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPITAL_FOMATION'\
		)
	~	
	~		|

Government_consumption_by_sector_and_region[REGION,SECTORS]=
	Final_demand_by_components[GOVERNMENT_DEMAND]*Share_of_each_sector_in_government_consumption\
		[SECTORS]
	~	
	~		|

SWITCH_GROWTH_SLOWDOWN_SP=
	0
	~	
	~	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , \
		'Switches' , 'SWITCH_GROWTH_SLOWDOWN_SP')
	|

Growth_slowdown=
	MIN(Growth_slowdown_fossil_fuels_rationing_factor,MIN(Growth_slowdown_labour_factor,\
		Growth_slowdown_land_rationing_factor))
	~	
	~		|

Desired_consumption_growth_rate[REGION,CLASS]=
	DESIRED_CONSUMPTION_GROWTH_RATE_SP[REGION,CLASS]*Growth_slowdown_factor
	~	
	~		|

Growth_slowdown_fossil_fuels_rationing_factor=
	if_then_else(SWITCH_FOSSIL_FUELS_RATIONING_SCARCITY_FACTOR=0,2,MIN(2,MAX(1,ZIDZ(Recoverable_resources_of_fossil_fuels\
		*MAXIMUM_SHARE_OF_EXTRACTABLE_FOSSIL_FUEL_RESOURCES_PER_YEAR_SP
	,SUM(Desired_primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS!])))))
	~	
	~		|

Growth_slowdown_labour_factor=
	if_then_else(SWITCH_LABOUR_SCARCITY_FACTOR=0,2,MIN(2,MAX(1,1-(Workforce_utilization_rate\
		-1))))
	~	
	~		|

Growth_slowdown_land_rationing_factor=
	if_then_else(SWITCH_LAND_SCARCITY_FACTOR_SP=0,2,MIN(2,MAX(1,ZIDZ(Disposable_land
	,SUM(Land_demand[SECTORIAL_LANDS!])+Land_demand[infrastructure]))))
	~	
	~		|

Desired_consumption_per_capita_variation[REGION,CLASS]=
	Desired_consumption_growth_rate[REGION,CLASS]*Desired_consumption_per_capita[REGION,\
		CLASS]
	~	euro/(person*Year*Year)
	~		|

Desired_final_demand_by_sector[SECTORS1]=
	(Desired_consumption_by_sector[SECTORS1]+Desired_gross_fixed_capital_formation_by_sector\
		[SECTORS1]+Desired_government_consumption_by_sector
	[SECTORS1])*Mortality_scarcity_factor
	~	million_euro/Year
	~		|

Desired_investment_by_sector[SECTORS]=
	MAX(0,INVESTMENT_SPEED_PARAMETER*(Delayed_time_step_output_by_sector[SECTORS]*Capital_intensity\
		[SECTORS]*(1+TARGET_EXCESS_CAPACITY_OF_THE_CAPITAL_STOCK
	)-Capital_stock[SECTORS])+Depreciation_by_sector[SECTORS])*Mortality_scarcity_factor
	~	million_euro/Year
	~	MAX(0,0.3*(ZIDZ(Delayed_time_step_output_by_sector[SECTORS],(1-0.2)*ZIDZ(1,Capital_in\
		tensity[SECTORS]))-Capital_stock[SECTORS])+Depreciation_by_sector[SECTORS])
		
		MAX(0,0.15*(Delayed_time_step_output_by_sector[SECTORS]*Capital_intensity[S\
		ECTORS]*(1+0.1)-Capital_stock[SECTORS])+Depreciation_by_sector[SECTORS])
	|

Air_pollution[AIR_POLLUTION_S]=
	(SUM(Output_by_sector[SECTORS!]*Air_pollution_sectorial_intensity[AIR_POLLUTION_S,SECTORS\
		!]))/10^9
	~	Mt
	~	original value from excel: kg -> convert to Mt
	|

A_matrix[SECTORS,SECTORS1] :EXCEPT:    [ENERGY_SECTORS,SSP_SECTORS]=
	A_matrix_before_application_of_factors[SECTORS,SECTORS1]*A_matrix_damage_factor[SECTORS1\
		] ~~|
A_matrix[ENERGY_SECTORS,SSP_SECTORS]=
	A_matrix_before_application_of_factors[ENERGY_SECTORS,SSP_SECTORS]*A_matrix_damage_factor\
		[SSP_SECTORS]*SSP_sectors_variation_factor[SSP_SECTORS]
	~	
	~		|

Air_pollution_sectorial_intensity[AIR_POLLUTION_S,SECTORS]=
	ZIDZ(Air_pollution_sectorial_intensity_before_damages[AIR_POLLUTION_S,SECTORS],1-Output_losses_due_to_climate_change\
		[SECTORS])
	~	
	~		|

Air_pollution_sectorial_intensity_before_damages[AIR_POLLUTION_S,SECTORS]=
	if_then_else(TARGET_AIR_POLLUTION_SECTORIAL_INTENSITY_SP[AIR_POLLUTION_S,SECTORS]=0,\
		INITIAL_AIR_POLLUTION_SECTORIAL_INTENSITY[AIR_POLLUTION_S,SECTORS]+RAMP(ZIDZ(TARGET_AIR_POLLUTION_SECTORIAL_INTENSITY_SP\
		[AIR_POLLUTION_S,SECTORS]-INITIAL_AIR_POLLUTION_SECTORIAL_INTENSITY[AIR_POLLUTION_S\
		,SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_AIR_POLLUTION_SECTORIAL_INTENSITY\
		[AIR_POLLUTION_S,SECTORS]*(1+Air_pollution_sectorial_intensity_growth_rate[AIR_POLLUTION_S\
		,SECTORS])^(Time-INITIAL_TIME))
	~	
	~		|

A_matrix_damage_factor[SECTORS] :EXCEPT:        [m_energy],[isengard],[m_material]=
	1 ~~|
A_matrix_damage_factor[m_energy]=
	Extraction_difficulty_factor ~~|
A_matrix_damage_factor[isengard]=
	Output_losses_factor_A_matrix ~~|
A_matrix_damage_factor[m_material]=
	Extraction_difficulty_factor
	~	
	~	if_then_else(Temperature_change_base_1850<1.4,1,ALPHA_OUTPUT_LOSSES_A_MATRIX* \
		Temperature_change_base_1850^2 - BETA_OUTPUT_LOSSES_A_MATRIX
		*Temperature_change_base_1850 + GAMMA_OUTPUT_LOSSES_A_MATRIX)
	|

Water_withdrawal_industrial_intensity_growth_rate[SECTORS]=
	ZIDZ(TARGET_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY_SP[SECTORS],INITIAL_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY\
		[SECTORS])^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Nitrogen_and_phosphorus_pollution_intensity_of_agriculture[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=
	ZIDZ(Nitrogen_and_phosphorus_pollution_intensity_of_agriculture_before_damages[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS],1-Output_losses_due_to_climate_change[SECTORS])
	~	
	~		|

Nitrogen_and_phosphorus_pollution_intensity_of_agriculture_before_damages[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=
	if_then_else(TARGET_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE_SP[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=0,INITIAL_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]+RAMP(ZIDZ(TARGET_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE_SP\
		[NITROGEN_PHOSPHORUS_POLLUTION,SECTORS]-INITIAL_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE\
		[NITROGEN_PHOSPHORUS_POLLUTION,SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE\
		[NITROGEN_PHOSPHORUS_POLLUTION,SECTORS]*(1+Nitrogen_and_phosphorus_pollution_intensity_of_agriculture_growth_rate\
		[NITROGEN_PHOSPHORUS_POLLUTION,SECTORS])^(Time-INITIAL_TIME))
	~	
	~		|

Nitrogen_and_phosphorus_pollution_intensity_of_agriculture_growth_rate[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=
	ZIDZ(TARGET_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE_SP[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS],INITIAL_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS])^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Nitrogen_and_phosphurus_pollution_of_agriculture[NITROGEN_PHOSPHORUS_POLLUTION]=
	(SUM(Nitrogen_and_phosphorus_pollution_intensity_of_agriculture[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS!]*Output_by_sector
	[SECTORS!]))/10^9*CORRECTION_P_SOIL[NITROGEN_PHOSPHORUS_POLLUTION]
	~	Mt
	~	original value in kg -> convert to Mt
	|

Urbanization_indicator=
	1-((Total_population_in_subsistence+Workers[isengard]*ALPHA_DEPENDENT_POPULATION*ALPHA_SUPPORTING_INDUSTRY\
		)/Total_population
	)
	~	
	~		|

TARGET_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_GREENHOUSE_GAS_EMISSIONS_INTENSITY')
	~	
	~		|

ALPHA_SUPPORTING_INDUSTRY=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Population' ,\
		 'ALPHA_SUPPORTING_INDUSTRY')
	~	
	~		|

Greenhouse_gas_emissions[EMISSIONS]=
	SUM(Greenhouse_gas_emissions_intensity[EMISSIONS,SECTORS!]*Output_by_sector[SECTORS!\
		])
	~	
	~		|

Greenhouse_gas_emissions_intensity[EMISSIONS,SECTORS]=
	ZIDZ(Greenhouse_gas_emissions_intensity_before_climate_damage[EMISSIONS,SECTORS],1-Output_losses_due_to_climate_change\
		[SECTORS])
	~	
	~		|

Greenhouse_gas_emissions_intensity_before_climate_damage[EMISSIONS,SECTORS]=
	if_then_else(TARGET_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS]=0,INITIAL_GREENHOUSE_GAS_EMISSIONS_INTENSITY\
		[EMISSIONS,SECTORS]+RAMP(ZIDZ(TARGET_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS\
		]-INITIAL_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS],2100-INITIAL_TIME),\
		 INITIAL_TIME , 2100),INITIAL_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS]\
		*(1+Greenhouse_gas_emissions_intensity_growth_rate[EMISSIONS,SECTORS])^(Time-INITIAL_TIME\
		))
	~	
	~		|

Greenhouse_gas_emissions_intensity_growth_rate[EMISSIONS,SECTORS]=
	ZIDZ(TARGET_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS]*10^6,INITIAL_GREENHOUSE_GAS_EMISSIONS_INTENSITY\
		[EMISSIONS,SECTORS]*10^6)^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Water_consumption_intensity_of_households_growth_rate=
	ZIDZ(TARGET_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS_SP,INITIAL_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS\
		)^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Water_consumption_of_households=
	SUM(Final_demand_by_components[CONSUMPTION_DEMAND!])*Water_consumption_intensity_of_households
	~	
	~		|

Water_withdrawal_intensity_of_households=
	SUM(Final_demand_by_components[CONSUMPTION_DEMAND!])*Water_withdrawal_intensity_of_household
	~	
	~		|

Water_industrial_consumption[WATER]=
	SUM(Output_by_sector[SECTORS!]*Water_consumption_industrial_intensity[WATER,SECTORS!\
		])
	~	
	~		|

Real_labour[SECTORS]=
	Labour_demand[SECTORS]*Scarcity_factor
	~	
	~		|

Water_industrial_withdrawal=
	SUM(Output_by_sector[SECTORS!]*Water_withdrawal_industrial_intensity[SECTORS!])
	~	
	~		|

Water_withdrawal_intensity_of_household_growth_rate=
	ZIDZ(TARGET_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD_SP,INITIAL_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD\
		)^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Water_use_by_type[green]=
	Water_industrial_consumption[green] ~~|
Water_use_by_type[blue]=
	Water_consumption_of_households+Water_industrial_consumption[blue]+Water_industrial_withdrawal\
		+Water_withdrawal_intensity_of_households
	~	
	~		|

Air_pollution_sectorial_intensity_growth_rate[AIR_POLLUTION_S,SECTORS]=
	ZIDZ(TARGET_AIR_POLLUTION_SECTORIAL_INTENSITY_SP[AIR_POLLUTION_S,SECTORS],INITIAL_AIR_POLLUTION_SECTORIAL_INTENSITY\
		[AIR_POLLUTION_S,SECTORS])^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Water_withdrawal_industrial_intensity_before_climate_damage[SECTORS]=
	if_then_else(TARGET_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY_SP[SECTORS]=0,INITIAL_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY\
		[SECTORS]+RAMP(ZIDZ(TARGET_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY_SP[SECTORS]-INITIAL_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY\
		[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY\
		[SECTORS]*(1+Water_withdrawal_industrial_intensity_growth_rate[SECTORS])^(Time-INITIAL_TIME\
		))
	~	
	~		|

Water_withdrawal_intensity_of_household=
	if_then_else(TARGET_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD_SP=0,INITIAL_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD\
		+RAMP(ZIDZ(TARGET_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD_SP-INITIAL_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD\
		,2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD\
		*(1+Water_withdrawal_intensity_of_household_growth_rate)^(Time-INITIAL_TIME))
	~	
	~		|

TARGET_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY_SP')
	~	
	~		|

TARGET_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD_SP')
	~	
	~		|

ALPHA_DEPENDENT_POPULATION=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Population' ,\
		 'ALPHA_DEPENDENT_POPULATION')
	~	
	~		|

Mortality_rate_over_five_years_subsistence[REGION,AGE_COHORTS] :EXCEPT:              \
		[REGION,C_95_plus]=
	MIN(5,YF_MORTALITY_RATE[AGE_COHORTS] + (Y0_MORTALITY_RATE[AGE_COHORTS] - YF_MORTALITY_RATE\
		[AGE_COHORTS]) * EXP(-EXP(LOG_ALPHA_MORTALITY_RATE
	[AGE_COHORTS]) * CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION])) ~~|
Mortality_rate_over_five_years_subsistence[REGION,C_95_plus]=
	1*5
	~	1/Year
	~		|

TARGET_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS_SP')
	~	
	~		|

Water_consumption_industrial_intensity_growth_rate[WATER,SECTORS]=
	ZIDZ(TARGET_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY_SP[WATER,SECTORS],INITIAL_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY\
		[WATER,SECTORS])^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

Total_real_labour=
	SUM(Real_labour[SECTORS!])
	~	
	~		|

Total_workers=
	SUM(Workers[SECTORS!])
	~	
	~		|

TARGET_AIR_POLLUTION_SECTORIAL_INTENSITY_SP[AIR_POLLUTION_S,SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_AIR_POLLUTION_SECTORIAL_INTENSITY')
	~	
	~		|

Water_withdrawal_industrial_intensity[SECTORS]=
	ZIDZ(Water_withdrawal_industrial_intensity_before_climate_damage[SECTORS],1-Output_losses_due_to_climate_change\
		[SECTORS])
	~	
	~		|

Mortality_rate_over_five_years_formal_economy[REGION,AGE_COHORTS] :EXCEPT:             \
		[REGION,C_95_plus]=
	MIN(5,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_MORTALITY_RATE_UNDER_SUBSISTENCE
	[AGE_COHORTS]+BETA_1_MORTALITY_RATE_UNDER_SUBSISTENCE[AGE_COHORTS]*Consumption_per_capita\
		[REGION,CLASS!],YF_MORTALITY_RATE
	[AGE_COHORTS] + (Y0_MORTALITY_RATE[AGE_COHORTS] - YF_MORTALITY_RATE[AGE_COHORTS]) * \
		EXP(-EXP(LOG_ALPHA_MORTALITY_RATE
	[AGE_COHORTS]) * (Consumption_per_capita[REGION,CLASS!]+Government_health_expenditure_per_capita\
		[REGION])))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Mortality_rate_over_five_years_formal_economy[REGION,C_95_plus]=
	1*5
	~	1/Year
	~		|

Water_consumption_intensity_of_households=
	if_then_else(TARGET_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS_SP=0,INITIAL_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS\
		+RAMP(ZIDZ(TARGET_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS_SP-INITIAL_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS\
		,2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS\
		*(1+Water_consumption_intensity_of_households_growth_rate)^(Time-INITIAL_TIME))
	~	
	~		|

TARGET_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY_SP[WATER,SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY_SP')
	~	
	~		|

Water_consumption_industrial_intensity[WATER,SECTORS]=
	ZIDZ(Water_consumption_industrial_intensity_before_climate_damage[WATER,SECTORS],1-Output_losses_due_to_climate_change\
		[SECTORS])
	~	
	~		|

Water_consumption_industrial_intensity_before_climate_damage[WATER,SECTORS]=
	if_then_else(TARGET_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY_SP[WATER,SECTORS]=0,INITIAL_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY\
		[WATER,SECTORS]+RAMP(ZIDZ(TARGET_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY_SP[WATER,SECTORS\
		]-INITIAL_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY[WATER,SECTORS],2100-INITIAL_TIME),\
		 INITIAL_TIME , 2100),INITIAL_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY[WATER,SECTORS]\
		*(1+Water_consumption_industrial_intensity_growth_rate[WATER,SECTORS])^(Time-INITIAL_TIME\
		))
	~	
	~		|

Workers[SECTORS]=
	ZIDZ(Real_labour[SECTORS],ANNUAL_WORKING_HOURS_SP)
	~	
	~		|

TARGET_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE_SP[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Stressors' , \
		'TARGET_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE_SP')
	~	
	~		|

Initial_nitrogen_and_phosphurus_pollution_of_agriculture[NITROGEN_PHOSPHORUS_POLLUTION\
		]= INITIAL(
	Nitrogen_and_phosphurus_pollution_of_agriculture[NITROGEN_PHOSPHORUS_POLLUTION])
	~	
	~		|

Lower_threshold_PBI_biogeochemical_flows_phosphurus=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_biogeochemical_flows_phosphurus'\
		)
	~	
	~		|

initial_output_by_sector[SECTORS]= INITIAL(
	Output_by_sector[SECTORS])
	~	
	~		|

Material_extraction_used[MATERIALS,SECTORS]=
	(MATERIAL_EXTRACTION_INTENSITY_USED[MATERIALS,SECTORS]*Output_by_sector[SECTORS]*CORRECTION_CHEMICAL_AND_FERTILIZER_MINERALS\
		[MATERIALS])/10^3
	~	Mt
	~	original value in kt -> conver to Mt
	|

Lower_threshold_PBI_land_system_change=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_land_system_change'\
		)
	~	
	~		|

Upper_threshold_PBI_biogeochemical_flows_nitrogen=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_biogeochemical_flows_nitrogen'\
		)
	~	
	~		|

Upper_threshold_PBI_biogeochemical_flows_phosphurus=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_biogeochemical_flows_phosphurus'\
		)
	~	
	~		|

Upper_threshold_PBI_biosphere_integrity=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_biosphere_integrity'\
		)
	~	
	~		|

Upper_threshold_PBI_Climate_CO2_concentration=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_Climate_CO2_concentration'\
		)
	~	
	~		|

Lower_threshold_PBI_biogeochemical_flows_nitrogen=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_biogeochemical_flows_nitrogen'\
		)
	~	
	~		|

PBI_biogeochemical_flows_phosphurus=
	ZIDZ(Nitrogen_and_phosphurus_pollution_of_agriculture[Phosphorus_soil],Initial_nitrogen_and_phosphurus_pollution_of_agriculture\
		[Phosphorus_soil])*100
	~	
	~		|

Lower_threshold_PBI_biosphere_integrity=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_biosphere_integrity'\
		)
	~	
	~		|

Initial_total_air_polution=
	INITIAL(Total_air_polution)
	~	
	~		|

PBI_Climate_CO2_radiative_forcing=
	ZIDZ(Effective_Radiative_Forcing,Initial_effective_Radiative_Forcing)*100
	~	
	~		|

PBI_freshwater_blue_water=
	ZIDZ(Water_consumption[blue],Initial_water_consumption[blue])*100
	~	
	~		|

Initial_water_consumption[WATER]=
	INITIAL(Water_consumption[WATER])
	~	
	~		|

Lower_threshold_PBI_ocean_acidification=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_ocean_acidification'\
		)
	~	
	~		|

Lower_threshold_PBI_ozone=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_ozone'\
		)
	~	
	~		|

PBI_ocean_acidification=
	100-(ZIDZ(Aragonite_saturation,Initial_aragonite_saturation)*100)+100
	~	
	~		|

Initial_material_extraction_used[MATERIALS,SECTORS]=
	INITIAL(Material_extraction_used[MATERIALS,SECTORS])
	~	
	~		|

Upper_threshold_PBI_Climate_CO2_radiative_forcing=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_Climate_CO2_radiative_forcing'\
		)
	~	
	~		|

Initial_atmospheric_concentrations_CO2= INITIAL(
	atmospheric_concentrations_CO2)
	~	
	~		|

PBI_Climate_CO2_concentration=
	ZIDZ(atmospheric_concentrations_CO2,Initial_atmospheric_concentrations_CO2)*100
	~	
	~		|

Lower_threshold_PBI_Climate_CO2_concentration=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_Climate_CO2_concentration'\
		)
	~	
	~		|

Lower_threshold_PBI_Climate_CO2_radiative_forcing=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_Climate_CO2_radiative_forcing'\
		)
	~	
	~		|

PBI_freshwater_green_water=
	ZIDZ(Water_consumption[green],Initial_water_consumption[green])*100
	~	
	~		|

PBI_land_system_change=
	100-ZIDZ((Land_distribution[forest_land]+Land_distribution[secondary_forest]+Land_distribution\
		[primary_forest])/((Initial_land_distribution[forest_land]+Initial_land_distribution\
		[secondary_forest]+Initial_land_distribution[primary_forest])/0.6),(Initial_land_distribution\
		[forest_land]+Initial_land_distribution[secondary_forest]+Initial_land_distribution\
		[primary_forest])/((Initial_land_distribution[forest_land]+Initial_land_distribution\
		[secondary_forest]+Initial_land_distribution[primary_forest])/0.6))*100+100
	~	
	~		|

PBI_novel_entities=
	ZIDZ(Output_by_sector[lot_alchemy],initial_output_by_sector[lot_alchemy])*100
	~	
	~		|

PBI_aerosol_loading=
	ZIDZ(Total_air_polution,Initial_total_air_polution)*100
	~	
	~		|

PBI_biogeochemical_flows_nitrogen=
	ZIDZ(SUM(Material_extraction_used[Chemical_and_fertilizer_minerals,SECTORS!]),SUM(Initial_material_extraction_used\
		[Chemical_and_fertilizer_minerals,SECTORS!]))*100
	~	
	~		|

Upper_threshold_PBI_ozone=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_ozone'\
		)
	~	
	~		|

Upper_threshold_PBI_land_system_change=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_land_system_change'\
		)
	~	
	~		|

Upper_threshold_PBI_novel_entities=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_novel_entities'\
		)
	~	
	~		|

CORRECTION_P_SOIL[NITROGEN_PHOSPHORUS_POLLUTION]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'CORRECTION_P_SOIL'\
		)
	~	
	~		|

Upper_threshold_PBI_ocean_acidification=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Upper_threshold_PBI_ocean_acidification'\
		)
	~	
	~		|

CORRECTION_CHEMICAL_AND_FERTILIZER_MINERALS[MATERIALS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'CORRECTION_CHEMICAL_AND_FERTILIZER_MINERALS'\
		)
	~	
	~		|

Lower_threshold_PBI_novel_entities=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Lower_threshold_PBI_novel_entities'\
		)
	~	
	~		|

Water_consumption[green]=
	Water_industrial_consumption[green] ~~|
Water_consumption[blue]=
	Water_industrial_consumption[blue]+Water_consumption_of_households
	~	
	~		|

Total_air_polution=
	SUM(Air_pollution[AIR_POLLUTION_S!])
	~	
	~		|

Initial_effective_Radiative_Forcing= INITIAL(
	Effective_Radiative_Forcing)
	~	
	~		|

PBI_ozone=
	100
	~	
	~		|

Initial_land_distribution[LAND]=
	INITIAL(Land_distribution[LAND])
	~	
	~		|

WEIGHTS_FOR_LAND_SYSTEM_CHANGE[LAND]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'WEIGHTS_FOR_LAND_SYSTEM_CHANGE'\
		)
	~	
	~		|

PBI_biosphere_integrity=
	ZIDZ(SUM(Land_distribution[LAND!]*WEIGHTS_FOR_LAND_SYSTEM_CHANGE[LAND!]),SUM(Initial_land_distribution\
		[LAND!]*WEIGHTS_FOR_LAND_SYSTEM_CHANGE[LAND!]))*100
	~	
	~		|

Initial_aragonite_saturation=
	INITIAL(Aragonite_saturation)
	~	
	~		|

ARAGONITE_SATURATION_CORRECTION_FACTOR=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'Aragonite_saturation_correction_factor'\
		)
	~	
	~	Richardson et al. Cite a study from 2015 for the aragonite value which \
		indicates a value of 2.8. The data is from 2012. Feely et al. (2023) \
		(https://doi.org/10.5670/oceanog.2023.222) indicate that sigma_arag \
		decreae by -0.08 per decade -> -0.008 per year -> -0.008*7 = -0,056 -> in \
		2019   2.8 - 0,056 = 2.744 -> a correction factor is applied to the model \
		(which is slightly too pessimistic with regard to sigma_arag levels) to \
		yield 2.744  -> original value in model: 2.62285  -> 2.744/2.62285 = \
		1,04619021293631
	|

Aragonite_saturation=
	(3.8731*pH_ocean^2-57.3718*pH_ocean+213.544)*ARAGONITE_SATURATION_CORRECTION_FACTOR
	~	
	~	Calculated Ocean Aragonite saturation.
		3.8731*pH_ocean^2-57.3718*pH_ocean+213.544
	|

I_A_matrix[SECTORS,SECTORS1]=
	I_matrix[SECTORS,SECTORS1]-A_matrix[SECTORS,SECTORS1]
	~	1
	~		|

Foodland_and_forest_priority_vector[LAND,ptype]=
	PTYPE_LAND_SP[LAND] ~~|
Foodland_and_forest_priority_vector[LAND,ppriority]=
	if_then_else(Delayed_TS_land_distribution[LAND]<=AMOUNT_OF_LAND_TO_PROTECT[LAND],PPRIORIY_PROTECTION_LAND_SP\
		[LAND],PPRIORITY_LAND_SP[LAND]) ~~|
Foodland_and_forest_priority_vector[LAND,pwidth]=
	PWIDTH_LAND_SP[LAND] ~~|
Foodland_and_forest_priority_vector[LAND,pextra]=
	PEXTRA_LAND_SP[LAND]
	~	
	~		|

A_matrix_before_application_of_factors[SECTORS,SECTORS1]=
	if_then_else(A_MATRIX_2100[SECTORS,SECTORS1]=0,INITIAL_A_MATRIX[SECTORS,SECTORS1]+RAMP\
		(ZIDZ(A_MATRIX_2100[SECTORS
	,SECTORS1]-INITIAL_A_MATRIX[SECTORS,SECTORS1],2100-INITIAL_TIME), INITIAL_TIME , 2100\
		),INITIAL_A_MATRIX[SECTORS,SECTORS1
	]*(1+Target_growth_rate_A_matrix[SECTORS,SECTORS1])^(Time-INITIAL_TIME))
	~	1
	~	(if_then_else(A_MATRIX_2100[SECTORS,SECTORS1]=0,INITIAL_A_MATRIX[SECTORS,SECTORS1]+RA\
		MP(ZIDZ(A_MATRIX_2100[SECTORS
		,SECTORS1]-INITIAL_A_MATRIX[SECTORS,SECTORS1],2100-INITIAL_TIME), INITIAL_TIME , \
		2100),INITIAL_A_MATRIX[SECTORS,SECTORS1
		]*(1+Target_growth_rate_A_matrix[SECTORS,SECTORS1])^(Time-INITIAL_TIME)))*A matrix \
		damage factor[SECTORS1]
		
		(if_then_else(A_MATRIX_2100[ENERGY SECTORS,SSP SECTORS]=0,INITIAL_A_MATRIX[ENERGY \
		SECTORS,SSP SECTORS]+RAMP(ZIDZ(A_MATRIX_2100
		[ENERGY SECTORS,SSP SECTORS]-INITIAL_A_MATRIX[ENERGY SECTORS,SSP \
		SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_A_MATRIX
		[ENERGY SECTORS,SSP SECTORS]*(1+Target_growth_rate_A_matrix[ENERGY SECTORS,SSP \
		SECTORS])^(Time-INITIAL_TIME)))*A matrix damage factor
		[SSP SECTORS]*SSP sectors variation factor[SSP SECTORS]
	|

Delayed_TS_output_per_capita_by_sector[SECTORS]= delay_fixed (
	Output_per_capita_by_sector[SECTORS], TIME_STEP, Initial_output_per_capita[SECTORS])
	~	
	~		|

SSP_sectors_variation_factor[SSP_SECTORS]=
	if_then_else(SWITCH_SSP_SECTORS_VARIATION_FACTOR=0,1,BETA_1_SSP[SSP_SECTORS]*(Delayed_TS_output_per_capita_by_sector\
		[SSP_SECTORS]*1e+06)^BETA_2_SSP
	[SSP_SECTORS]+BETA_3_SSP[SSP_SECTORS])
	~	
	~		|

PPRIORIY_PROTECTION_LAND_SP[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'PPRIORIY_PROTECTION_LAND_SP'\
		)
	~	
	~		|

Initial_output_per_capita[SECTORS]=
	ZIDZ(INITIAL_OUTPUT[SECTORS],SUM(INITIAL_POPULATION_IN_FORMAL_ECONOMY[REGION!,AGE_COHORTS\
		!]+INITIAL_POPULATION_IN_SUBSISTENCE[REGION!,AGE_COHORTS!]))
	~	
	~		|

Delayed_TS_land_distribution[LAND]=
	delay_fixed(Land_distribution[LAND],TIME_STEP ,Disposable_land)
	~	
	~		|

AMOUNT_OF_LAND_TO_PROTECT[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'AMOUNT_OF_LAND_TO_PROTECT'\
		)
	~	
	~		|

Total_population=
	Total_population_in_formal_economy+Total_population_in_subsistence
	~	
	~		|

BETA_3_SSP[SSP_SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'BETA_3_SSP'\
		)
	~	
	~		|

BETA_2_SSP[SSP_SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'BETA_2_SSP'\
		)
	~	
	~		|

SWITCH_SSP_SECTORS_VARIATION_FACTOR=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_SSP_SECTORS_VARIATION_FACTOR'\
		)
	~	
	~		|

ENERGY_SECTORS:
	m_energy,
	shire_energy,
	lot_ff,
	lot_nuc,
	lot_re_hydro,
	lot_re_wind,
	lot_re_bio,
	lot_re_PV,
	lot_re_stherm,
	lot_re_tide,
	lot_re_gtherm
	~	
	~		|

SSP_SECTORS:
	m_energy,
	dale,
	minas_tir,
	shire_energy,
	lot_ff,
	lot_nuc,
	lot_re_hydro,
	lot_re_wind,
	lot_re_PV,
	rohan
	~	
	~		|

Output_per_capita_by_sector[SECTORS]=
	ZIDZ(Output_by_sector[SECTORS],Total_population)
	~	
	~		|

BETA_1_SSP[SSP_SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'BETA1_SSP'\
		)
	~	
	~		|

Initial_capital_stock[SECTORS]=
	INITIAL_CAPITAL_INTENSITY[SECTORS]*INITIAL_OUTPUT[SECTORS]*INITIAL_CAPITAL_FACTOR_TO_ADJUST_INVESTMENTS
	~	
	~	0.76497
	|

INITIAL_CAPITAL_FACTOR_TO_ADJUST_INVESTMENTS=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_CAPITAL_FACTOR_TO_ADJUST_INVESTMENTS'\
		)
	~	
	~		|

INVESTMENT_SPEED_PARAMETER=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INVESTMENT_SPEED_PARAMETER'\
		)
	~	
	~		|

TARGET_EXCESS_CAPACITY_OF_THE_CAPITAL_STOCK=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'TARGET_EXCESS_CAPACITY_OF_THE_CAPITAL_STOCK'\
		)
	~	
	~		|

Fossil_fuels_rationing_scarcity_factor=
	if_then_else(SWITCH_FOSSIL_FUELS_RATIONING_SCARCITY_FACTOR=0:OR:SUM(Desired_primary_energy_of_fossil_fuels_by_type\
		[FOSSIL_FUELS!])=0,1,MIN(1,ZIDZ(Recoverable_resources_of_fossil_fuels*MAXIMUM_SHARE_OF_EXTRACTABLE_FOSSIL_FUEL_RESOURCES_PER_YEAR_SP\
		,SUM(Desired_primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS!]))))
	~	
	~	MIN(1,ZIDZ(SUM(Desired_primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS!]),
		Recoverable_resources_of_fossil_fuels*MAXIMUM_SHARE_OF_EXTRACTABLE_FOSSIL_F\
		UEL_RESOURCES_PER_YEAR_SP))
	|

ratio_capital_output_total_economy=
	ZIDZ(SUM(Capital_stock[SECTORS!]),SUM(Output_by_sector[SECTORS!]))
	~	
	~		|

SWITCH_FOSSIL_FUELS_RATIONING_SCARCITY_FACTOR=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_FOSSIL_FUELS_RATIONING_SCARCITY_FACTOR'\
		)
	~	
	~		|

ratio_capital_output[SECTORS]=
	ZIDZ(Capital_stock[SECTORS],Output_by_sector[SECTORS])
	~	
	~		|

Total_anthropogenic_non_CO2_emissions_in_CO2_equivalents=
	Global_anthropogenic_CH4_emissions_in_CO2equivalents+Global_anthropogenic_HFC_emissions_in_CO2equivalents\
		+Global_anthropogenic_N2O_emissions_in_CO2equivalents+Global_anthropogenic_PFC_emissions_in_CO2equivalents\
		+Global_anthropogenic_SF6_emissions_in_CO2equivalents
	~	GTCO2e/Year
	~		|

Global_anthropogenic_HFC_emissions_in_CO2equivalents=
	Global_HFC_emissions[HFC134a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC134a\
		] , GWP_100_year
	[HFC134a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC23]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC23\
		] , GWP_100_year
	[HFC23])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC32]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC32\
		] , GWP_100_year
	[HFC32])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC125]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC125\
		] , GWP_100_year
	[HFC125])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC143a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC143a\
		] , GWP_100_year
	[HFC143a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC152a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC152a\
		] , GWP_100_year
	[HFC152a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC227ea]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC227ea] , GWP_100_year
	[HFC227ea])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC245ca]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC245ca] , GWP_100_year
	[HFC245ca])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC4310mee]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[HFC4310mee] , GWP_100_year
	[HFC4310mee])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT]
	~	GTCO2e/Year
	~		|

Global_anthropogenic_N2O_emissions_in_CO2equivalents=
	Anthropogenic_N2O_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[N2O\
		] , GWP_100_year
	[N2O])/MATRIX_UNIT_PREFIXES[giga,mega]
	~	GTCO2e/Year
	~		|

Global_anthropogenic_PFC_emissions_in_CO2equivalents=
	Anthropogenic_PFC_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[PFCs\
		] , GWP_100_year[PFCs]
	)/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT]
	~	GTCO2e/Year
	~		|

Global_anthropogenic_CH4_emissions_in_CO2equivalents=
	Global_anthropogenic_CH4_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[CH4] , GWP_100_year
	[CH4])/MATRIX_UNIT_PREFIXES[giga,mega]
	~	GTCO2e/Year
	~		|

Global_anthropogenic_SF6_emissions_in_CO2equivalents=
	Global_SF6_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[SF6] , GWP_100_year\
		[SF6])/
	MATRIX_UNIT_PREFIXES[giga,BASE_UNIT]
	~	GTCO2e/Year
	~		|

Extra_GFCF_due_to_sea_level_rise[SECTORS]=
	if_then_else(SWITCH_DAMAGES_SEA_LEVEL_RISE_SP=0, 0, if_then_else(Threshold_of_2°C_exceeded\
		=1:AND:Accumulated_extra_GFCF_due_to_sea_level_rise[SECTORS]<=TOTAL_EXTRA_GFCF_DUE_TO_SEA_LEVEL_RISE_SP\
		[SECTORS],TOTAL_EXTRA_GFCF_DUE_TO_SEA_LEVEL_RISE_SP[SECTORS]/40,0))
	~	
	~		|

Extra_subsistence_land_intensity_due_to_climate_damage=
	if_then_else(SWITCH_SUBSISTENCE_LAND_INTENSITY_DUE_TO_CLIMATE_CHANGE_SP=0, 0, ALPHA_LAND_SUBSISTENCE_DAMAGE_SP\
		*(Temperature_change_base_1850-1))
	~	
	~		|

Total_population_in_subsistence=
	SUM(Total_population_in_subsistence_by_region[REGION!])
	~	
	~		|

Total_population_in_subsistence_by_region[REGION]=
	SUM(Population_in_subsistence[REGION,AGE_COHORTS!])
	~	
	~		|

Total_anthropogenic_CO2_emissions=
	Anthropogenic_CO2_Emissions_wo_LUC+Anthropogenic_LUC_CO2_Emissions
	~	MtCO2/Year
	~		|

Average_age_in_formal_economy_by_region[REGION]=
	ZIDZ(SUM(AGE_BY_COHORT[AGE_COHORTS!]*Population_in_formal_economy[REGION,AGE_COHORTS\
		!]),SUM(Population_in_formal_economy[REGION,AGE_COHORTS!]))
	~	
	~		|

Average_age_in_subsistence_by_region[REGION]=
	ZIDZ(SUM(AGE_BY_COHORT[AGE_COHORTS!]*Population_in_subsistence[REGION,AGE_COHORTS!])\
		,SUM(Population_in_subsistence[REGION,AGE_COHORTS!]))
	~	
	~		|

Land_loss_caused_by_climate_change=
	if_then_else(SWITCH_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP=0, 0, MAXIMUM_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP\
		/9*(Temperature_change_base_1850-1)^2)
	~	
	~		|

Depreciation_rate_caused_by_climate_change[SECTORS]=
	if_then_else(SWITCH_DEPRECIATION_RATE_CAUSED_BY_CLIMATE_CHANGE_SP=0, 0, SECTORAL_SHARES_OF_DAMAGES_IN_CAPITAL_STOCK_SP\
		[SECTORS]*(Temperature_change_base_1850-1)^2/9)
	~	
	~		|

Depreciation_rate_caused_by_sea_level_rise=
	if_then_else(SWITCH_DAMAGES_SEA_LEVEL_RISE_SP=0, 0, Depreciation_rate_caused_by_sea_level_rise_2°C\
		+Depreciation_rate_caused_by_sea_level_rise_3°C+Depreciation_rate_caused_by_sea_level_rise_4°C\
		)
	~	
	~		|

SWITCH_FOSSIL_FUELS_EXTRACTION_DIFFICULTY_FACTOR_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_FOSSIL_FUELS_EXTRACTION_DIFFICULTY_FACTOR_SP'\
		)
	~	
	~		|

Final_energy_use_by_type[ENERGY]=
	SUM(Final_energy_use_by_sector_and_type[ENERGY,SECTORS!])
	~	
	~		|

SWITCH_LABOUR_SCARCITY_FACTOR=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_LABOUR_SCARCITY_FACTOR'\
		)
	~	
	~		|

SWITCH_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP'\
		)
	~	
	~		|

SWITCH_LAND_SCARCITY_FACTOR_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_LAND_SCARCITY_FACTOR_SP'\
		)
	~	
	~		|

AGE_BY_COHORT[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'AGE_BY_COHORT'\
		)
	~	
	~		|

Output_losses_due_to_climate_change[SECTORS]=
	if_then_else(SWITCH_OUTPUT_LOSS_FACTOR_SP=0, 0, OUTPUT_LOSSES_FACTOR_SP[SECTORS]*(Temperature_change_base_1850\
		-1)/3)
	~	
	~		|

Labour_scarcity_factor=
	if_then_else(SWITCH_LABOUR_SCARCITY_FACTOR=0,1,MAX(0,MIN(1,1-(Workforce_utilization_rate\
		-1))))
	~	
	~	if_then_else(Workforce_utilization_rate<1,1,MAX(0,MIN(1,1-(Workforce_utilization_rate\
		-1))))
		if_then_else(SWITCH_LABOUR_SCARCITY_FACTOR=0,1,MAX(0,MIN(1,1-(Workforce_uti\
		lization_rate-1))))
	|

SWITCH_SUBSISTENCE_LAND_INTENSITY_DUE_TO_CLIMATE_CHANGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_SUBSISTENCE_LAND_INTENSITY_DUE_TO_CLIMATE_CHANGE_SP'\
		)
	~	
	~		|

Share_of_each_sector_in_consumption[REGION,CLASS,SECTORS]=
	if_then_else(Desired_consumption_per_capita[REGION,CLASS]<CONSUMPTION_PER_CAPITA_1,Consumption_share_1\
		[SECTORS],
	
	if_then_else(Desired_consumption_per_capita[REGION,CLASS]<CONSUMPTION_PER_CAPITA_2,Consumption_share_1\
		[SECTORS]+(Consumption_share_2
	[SECTORS]-Consumption_share_1[SECTORS])/(CONSUMPTION_PER_CAPITA_2-CONSUMPTION_PER_CAPITA_1\
		)*(Desired_consumption_per_capita
	[REGION,CLASS]-CONSUMPTION_PER_CAPITA_1),
	
	if_then_else(Desired_consumption_per_capita[REGION,CLASS]<CONSUMPTION_PER_CAPITA_3,Consumption_share_2\
		[SECTORS]+(Consumption_share_3[SECTORS]-Consumption_share_2[SECTORS])/(CONSUMPTION_PER_CAPITA_3\
		-CONSUMPTION_PER_CAPITA_2)*(Desired_consumption_per_capita
	[REGION,CLASS]-CONSUMPTION_PER_CAPITA_2),
	
	Consumption_share_3[SECTORS])))
	~	1
	~		|

Extraction_difficulty_factor=
	if_then_else(
	SWITCH_FOSSIL_FUELS_EXTRACTION_DIFFICULTY_FACTOR_SP=0,1,
	MAX(1,BETA_0_EXTRACTION_SP*EXP(BETA_1_EXTRACTION_SP* 
	(1-MAX
	(0,
	((Recoverable_resources_of_fossil_fuels)/INITIAL_RECOVERABLE_RESOURCES_OF_FOSSIL_FUELS_SP\
		)
	)
	)
	)
	)
	)
	~	
	~	linear:
		if_then_else(SWITCH_FOSSIL_FUELS_EXTRACTION_DIFFICULTY_FACTOR_SP=0,1,MAX(1,\
		BETA_0_EXTRACTION_SP+BETA_1_EXTRACTION_SP*(1-MAX(0,Recoverable_resources_of\
		_fossil_fuels/INITIAL_RECOVERABLE_RESOURCES_OF_FOSSIL_FUELS_SP))))
	|

Damages_on_labour_productivity_produced_by_heat[SECTORS]=
	if_then_else(SWITCH_DAMAGES_ON_LABOUR_PRODUCTIVITY_BY_HEAT_SP=0, 0,ALPHA_DAMAGE_LABOUR_PRODUCTIVITY_SP\
		[SECTORS]*(Temperature_change_base_1850-1)^2/4)
	~	
	~		|

SWITCH_DAMAGES_SEA_LEVEL_RISE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_SP'\
		)
	~	
	~		|

SWITCH_LOSSES_LABOUR_SUPPLY_BY_HEAT_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_LOSSES_LABOUR_SUPPLY_BY_HEAT_SP'\
		)
	~	
	~		|

Global_HFC_emissions[HFC134a]=
	Anthropogenic_HFC_Emissions ~~|
Global_HFC_emissions[HFC23]=
	0 ~~|
Global_HFC_emissions[HFC32]=
	0 ~~|
Global_HFC_emissions[HFC125]=
	0 ~~|
Global_HFC_emissions[HFC143a]=
	0 ~~|
Global_HFC_emissions[HFC152a]=
	0 ~~|
Global_HFC_emissions[HFC227ea]=
	0 ~~|
Global_HFC_emissions[HFC245ca]=
	0 ~~|
Global_HFC_emissions[HFC4310mee]=
	0
	~	tons/Year
	~	Historic data + projections "Representative Concentration Pathways" (RCPs, see \
		http://tntcat.iiasa.ac.at:8787/RcpDb/dsd?Action=htmlpage&page=compare)
		Choose RCP:
		1. RCP 2.6
		2. RCP 4.5
		3. RCP 6.0
		4. RCP 8.5
	|

Losses_of_maximum_labour_supply_due_to_heat=
	if_then_else(SWITCH_LOSSES_LABOUR_SUPPLY_BY_HEAT_SP=0, 0,ALPHA_DAMAGE_LABOUR_SUPPLY_SP\
		*(1/9)*(Temperature_change_base_1850-1)^2)
	~	
	~		|

SWITCH_DEPRECIATION_RATE_CAUSED_BY_CLIMATE_CHANGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_DEPRECIATION_RATE_CAUSED_BY_CLIMATE_CHANGE_SP'\
		)
	~	
	~		|

Output_losses_factor_A_matrix=
	if_then_else(SWITCH_OUTPUT_LOSS_FACTOR_SP=0, 1, if_then_else(Temperature_change_base_1850\
		<1.4,1,ALPHA_OUTPUT_LOSSES_A_MATRIX_SP* Temperature_change_base_1850^2 - BETA_OUTPUT_LOSSES_A_MATRIX_SP\
		*Temperature_change_base_1850 + GAMMA_OUTPUT_LOSSES_A_MATRIX_SP))
	~	
	~		|

Foodland_loss_caused_by_climate_change=
	if_then_else(SWITCH_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP=0, 0, MAXIMUM_FOODLAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP\
		/9*(Temperature_change_base_1850-1)^2)
	~	
	~		|

SWITCH_DAMAGES_ON_LABOUR_PRODUCTIVITY_BY_HEAT_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_DAMAGES_ON_LABOUR_PRODUCTIVITY_BY_HEAT_SP'\
		)
	~	
	~		|

SWITCH_OUTPUT_LOSS_FACTOR_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Switches' , 'SWITCH_OUTPUT_LOSS_FACTOR_SP'\
		)
	~	
	~		|

Land_scarcity_factor=
	if_then_else(SWITCH_LAND_SCARCITY_FACTOR_SP=0,1,VMIN(Sectorial_lands_scarcity_factor\
		[SECTORIAL_LANDS!]))
	~	
	~	VMIN(Sectorial_lands_scarcity_factor[SECTORIAL_LANDS!])
	|

TARGET_CONSUMPTION_SHARE_1[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TARGET_CONSUMPTION_SHARE_1'\
		)
	~	
	~		|

TARGET_CONSUMPTION_SHARE_2[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TARGET_CONSUMPTION_SHARE_2'\
		)
	~	
	~		|

TARGET_CONSUMPTION_SHARE_3[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TARGET_CONSUMPTION_SHARE_3'\
		)
	~	
	~		|

Consumption_share_2[SECTORS]=
	INITIAL_CONSUMPTION_SHARE_2[SECTORS]+RAMP(ZIDZ(TARGET_CONSUMPTION_SHARE_2[SECTORS]-INITIAL_CONSUMPTION_SHARE_2\
		[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100)
	~	
	~		|

Consumption_share_1[SECTORS]=
	INITIAL_CONSUMPTION_SHARE_1[SECTORS]+RAMP(ZIDZ(TARGET_CONSUMPTION_SHARE_1[SECTORS]-INITIAL_CONSUMPTION_SHARE_1\
		[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100)
	~	
	~		|

Consumption_share_3[SECTORS]=
	INITIAL_CONSUMPTION_SHARE_3[SECTORS]+RAMP(ZIDZ(TARGET_CONSUMPTION_SHARE_3[SECTORS]-INITIAL_CONSUMPTION_SHARE_3\
		[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100)
	~	
	~		|

Labour_intensity[SECTORS] :EXCEPT:      [m_energy]=
	ZIDZ(1,ZIDZ(1,Labour_intensity_before_damage[SECTORS])*(1-Damages_on_labour_productivity_produced_by_heat\
		[SECTORS]-Output_losses_due_to_climate_change[SECTORS])) ~~|
Labour_intensity[m_energy]=
	ZIDZ(1,ZIDZ(1,Labour_intensity_before_damage[m_energy])*(1-Damages_on_labour_productivity_produced_by_heat\
		[m_energy]-Output_losses_due_to_climate_change[m_energy]))*Extraction_difficulty_factor
	~	
	~		|

Sectorial_land_intensities[SECTORIAL_LANDS,SECTORS]=
	ZIDZ(1,ZIDZ(1,Sectorial_land_intensities_before_damage[SECTORIAL_LANDS,SECTORS])*(1-\
		Output_losses_due_to_climate_change[SECTORS]))
	~	
	~	1/((1/Labour_intensity_before_damage[SECTORS])*(1-ALPHA_DAMAGE_LABOUR_PRODU\
		CTIVITY[SECTORS]*(Temperature_change-1)^2/4-OUTPUT_LOSSES_FACTOR[SECTORS]*(\
		Temperature_change-1)/3))
	|

MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_2°C_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_2°C_SP'\
		)
	~	
	~		|

MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_4°C_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_4°C_SP'\
		)
	~	
	~		|

Target_capital_intensity_growth_rate[SECTORS]=
	ZIDZ(CAPITAL_INTENSITY_2100_SP[SECTORS],INITIAL_CAPITAL_INTENSITY[SECTORS])^(1/(2100\
		-INITIAL_TIME))-1
	~	
	~		|

Maximum_labour_supply=
	SUM(Population_in_formal_economy[REGION!,WORKING_AGE_POPULATION!])*ANNUAL_WORKING_HOURS_SP\
		*(1-Losses_of_maximum_labour_supply_due_to_heat)*MAXIMUM_PARTICIPATION_RATE_SP
	~	
	~		|

TARGET_SUBSISTENCE_LAND_INTENSITY_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'TARGET_SUBSISTENCE_LAND_INTENSITY'\
		)
	~	
	~		|

SIGMA_SLR_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'SIGMA_SLR_SP'\
		)
	~	
	~		|

Capital_intensity[SECTORS] :EXCEPT:     [m_energy]=
	ZIDZ(1,ZIDZ(1,Capital_intensity_before_damage[SECTORS])*(1-Output_losses_due_to_climate_change\
		[SECTORS])) ~~|
Capital_intensity[m_energy]=
	Capital_intensity_before_damage[m_energy]*Extraction_difficulty_factor
	~	
	~		|

Capital_intensity_before_damage[SECTORS]=
	(if_then_else(CAPITAL_INTENSITY_2100_SP[SECTORS]=0,INITIAL_CAPITAL_INTENSITY[SECTORS\
		]+RAMP(ZIDZ(CAPITAL_INTENSITY_2100_SP[SECTORS]-INITIAL_CAPITAL_INTENSITY[SECTORS],2100\
		-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_CAPITAL_INTENSITY[SECTORS]*(1+Target_capital_intensity_growth_rate\
		[SECTORS])^(Time-INITIAL_TIME)))
	~	
	~	INITIAL_CAPITAL_INTENSITY[SECTORS]+RAMP(ZIDZ(CAPITAL_INTENSITY_2100_SP[SECT\
		ORS]-INITIAL_CAPITAL_INTENSITY[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , \
		2100)
	|

Depreciation_rate_caused_by_sea_level_rise_2°C=
	MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_2°C_SP*EXP(-ZIDZ((Time-10-Year_threshold_of_2°C_exceeded\
		)^2,SIGMA_SLR_SP))
	~	
	~	if_then_else(Threshold of 2°C exceeded=1:AND:Accumulated depreciation rate caused \
		by see level rise 2°C<=0.01*10,0.01
		,0)
		
		0.02*EXP(-ZIDZ((Time-5-Year_threshold_of_2°C_exceeded)^2,2*0.199471^2))
	|

Depreciation_rate_caused_by_sea_level_rise_3°C=
	MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_3°C_SP*EXP(-ZIDZ((Time-10-Year_threshold_of_3°C_exceeded\
		)^2,SIGMA_SLR_SP))
	~	
	~	if_then_else(Threshold of 3°C exceeded=1:AND:Accumulated depreciation rate caused \
		by see level rise 3°C<=0.015*10,0.015
		,0)
	|

Depreciation_rate_caused_by_sea_level_rise_4°C=
	MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_4°C_SP*EXP(-ZIDZ((Time-10-Year_threshold_of_4°C_exceeded\
		)^2,SIGMA_SLR_SP))
	~	
	~	if_then_else(Threshold of 4°C exceeded=1:AND:Accumulated depreciation rate caused \
		by see level rise 4°C<=0.02*10,0.02
		,0)
	|

Subsistence_land_intensity_growth_rate=
	ZIDZ(TARGET_SUBSISTENCE_LAND_INTENSITY_SP,INITIAL_SUBSISTENCE_LAND_INTENSITY)^(1/(2100\
		-INITIAL_TIME))-1
	~	
	~		|

MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_3°C_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'MAXIMUM_DEPRECIATION_RATE_CAUSED_BY_SEA_LEVEL_RISE_3°C_SP'\
		)
	~	
	~		|

Subsistence_land_intensity=
	Subsistence_land_intensity_before_damage+Extra_subsistence_land_intensity_due_to_climate_damage
	~	
	~		|

Subsistence_land_intensity_before_damage=
	if_then_else(TARGET_SUBSISTENCE_LAND_INTENSITY_SP=0,INITIAL_SUBSISTENCE_LAND_INTENSITY\
		+RAMP(ZIDZ(TARGET_SUBSISTENCE_LAND_INTENSITY_SP-INITIAL_SUBSISTENCE_LAND_INTENSITY,\
		2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_SUBSISTENCE_LAND_INTENSITY*(1+Subsistence_land_intensity_growth_rate\
		)^(Time-INITIAL_TIME))
	~	
	~		|

Foodland_demand_for_subsistence=
	People_that_desire_to_be_in_subsistence*Subsistence_land_intensity
	~	
	~		|

Desired_government_consumption_by_region[REGION]=
	Desired_consumption_by_region[REGION]*GOVERNMENT_CONSUMPTION_AS_SHARE_OF_HOUSEHOLDS_CONSUMPTION_BY_REGION\
		[REGION]
	~	million_euro/Year
	~		|

INITIAL_USED_FOREST=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'INITIAL_USED_FOREST*'\
		)
	~	
	~		|

rate_of_people_that_want_to_incorporate_to_subsistence[REGION,CLASS]=
	MAX(0,MIN(0.1,BETA_0_FORMAL_ECONOMY_TO_SUBSISTENCE_SP-BETA_1_FORMAL_ECONOMY_TO_SUBSISTENCE_SP
	*Delayed_TS_consumption_per_capita[REGION,CLASS]))
	~	
	~		|

Land_use_change_emissions_by_land[LAND_EMISSIONS]=
	Land_use_change_generating_emissions[LAND_EMISSIONS]*LAND_USE_CHANGE_EMISSIONS_INTENSITY\
		[LAND_EMISSIONS]
	~	
	~		|

Delayed_TS_consumption_per_capita[REGION,CLASS]=
	delay_fixed(Consumption_per_capita[REGION,CLASS], TIME_STEP , INITIAL_CONSUMPTION_PER_CAPITA\
		[REGION,CLASS])
	~	
	~		|

Sectorial_lands_scarcity_factor[SECTORIAL_LANDS]=
	if_then_else(Land_demand[SECTORIAL_LANDS]=0,1,ZIDZ(Land_distribution[SECTORIAL_LANDS\
		],Land_demand[SECTORIAL_LANDS]))
	~	
	~		|

Delayed_TS_used_forest= delay_fixed (
	Land_distribution[forest_land], TIME_STEP , INITIAL_USED_FOREST)
	~	
	~		|

ALPHA_LAND_SUBSISTENCE_DAMAGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'ALPHA_LAND_SUBSISTENCE_DAMAGE'\
		)
	~	
	~		|

People_that_desire_to_be_in_subsistence=
	SUM(Population_in_formal_economy[REGION!,AGE_COHORTS!]*SHARE_OF_POPULATION_PER_CLASS\
		[CLASS!]*rate_of_people_that_want_to_incorporate_to_subsistence
	[REGION!,CLASS!])+SUM(Population_in_subsistence[REGION!,AGE_COHORTS!])
	~	
	~	SUM(Population[REGION!,AGE \
		COHORTS!]*SHARE_OF_POPULATION_PER_CLASS[CLASS!]*rate_of_people_that_want_to\
		_incorporate_to_subsistence
		[REGION!,CLASS!])-SUM(Population_in_subsistence[REGION!,AGE \
		COHORTS!]*rate_of_people_that_want_incorporate_to_formal_economy
		[REGION!])
	|

Land_demand[infrastructure]=
	Land_demand_for_human_use[infrastructure] ~~|
Land_demand[energy_land]=
	Land_demand_for_human_use[energy_land] ~~|
Land_demand[food_land_capitalism]=
	Land_demand_for_human_use[food_land_capitalism] ~~|
Land_demand[food_land_subsistence]=
	Land_demand_for_human_use[food_land_subsistence] ~~|
Land_demand[primary_forest]=
	Delayed_TS_unused_forest[primary_forest] ~~|
Land_demand[secondary_forest]=
	MAX(0,Delayed_TS_unused_forest[secondary_forest]+Delayed_TS_used_forest-Land_demand_for_human_use\
		[forest_land]) ~~|
Land_demand[other_land]=
	Land_demand_for_human_use[other_land] ~~|
Land_demand[shrub]=
	Disposable_land ~~|
Land_demand[forest_land]=
	Land_demand_for_human_use[forest_land]
	~	
	~		|

BETA_OUTPUT_LOSSES_A_MATRIX_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'BETA_OUTPUT_LOSSES_A_MATRIX'\
		)
	~	
	~		|

Natural_PFC_emissions=
	Preindustrial_PFC/Time_Const_for_PFC
	~	tons/Year
	~		|

rate_of_people_that_want_incorporate_to_formal_economy[REGION]=
	MAX(0,MIN(0.1,BETA_1_SUBSISTENCE_TO_FORMAL_ECONOMY_SP*(Delayed_TS_consumption_per_capita\
		[REGION,low]-CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE
	[REGION])))
	~	
	~		|

Land_generating_emissions_increase[LAND_EMISSIONS]=
	MAX(0,Land_variation[LAND_EMISSIONS])
	~	
	~	MAX(0,Land_variation[LAND_EMISSIONS]*ZIDZ(SUM(Land_variation[FOREST_LAND_S!\
		]),SUM(Land_variation[LAND_EMISSIONS!])))
	|

Scarcity_factor=
	MAX(0,MIN(MIN(MIN(MIN(Land_scarcity_factor,Labour_scarcity_factor),Fossil_fuels_rationing_scarcity_factor\
		),Mortality_scarcity_factor),1))
	~	
	~		|

Subsistence_to_formal_economy[REGION,AGE_COHORTS]=
	MAX(Population_in_subsistence[REGION,AGE_COHORTS]*rate_of_people_that_want_incorporate_to_formal_economy\
		[REGION],ZIDZ(MAX(0,SUM(Population_in_subsistence[REGION!,AGE_COHORTS!])-Maximum_population_in_subsistence\
		),SUM(Population_in_subsistence[REGION!,AGE_COHORTS!]))*Population_in_subsistence[REGION\
		,AGE_COHORTS])
	~	
	~		|

GAMMA_OUTPUT_LOSSES_A_MATRIX_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'GAMMA_OUTPUT_LOSSES_A_MATRIX'\
		)
	~	
	~		|

Forest_land_reduction=
	MAX(0,-(Land_variation[forest_land]+Land_variation[primary_forest]+Land_variation[secondary_forest\
		]))
	~	
	~		|

Land_use_change_generating_emissions[LAND_EMISSIONS]=
	ZIDZ(Land_generating_emissions_increase[LAND_EMISSIONS],SUM(Land_generating_emissions_increase\
		[LAND_EMISSIONS!]))*Forest_land_reduction
	~	
	~		|

ALPHA_OUTPUT_LOSSES_A_MATRIX_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'ALPHA_OUTPUT_LOSSES_A_MATRIX'\
		)
	~	
	~		|

Delayed_TS_unused_forest[UNUSED_FOREST]=
	delay_fixed(Land_distribution[UNUSED_FOREST], TIME_STEP , INITIAL_UNUSED_FOREST[UNUSED_FOREST\
		])
	~	
	~		|

Total_capital_stock=
	SUM(Capital_stock[SECTORS!])
	~	
	~		|

Total_initial_output=
	SUM(INITIAL_OUTPUT[SECTORS!])
	~	
	~		|

Total_births_in_subsistence=
	SUM(Births_subsistence[REGION!])
	~	
	~		|

Total_deaths_in_subsistence=
	SUM(Deaths_subsistence[REGION!,AGE_COHORTS!])
	~	
	~		|

Flow_threshold_of_3°C_exceeded=
	if_then_else(Temperature_change_base_1850>=3:AND:Year_threshold_of_3°C_exceeded=0,Time\
		/TIME_STEP,0)
	~	
	~		|

Flow_threshold_of_4°C_exceeded=
	if_then_else(Temperature_change_base_1850>=4:AND:Year_threshold_of_4°C_exceeded=0,Time\
		/TIME_STEP,0)
	~	
	~		|

Flow_threshold_of_2°C_exceeded=
	if_then_else(Temperature_change_base_1850>=2:AND:Year_threshold_of_2°C_exceeded=0,Time\
		/TIME_STEP,0)
	~	
	~		|

Primary_energy_of_uranium=
	Desired_primary_energy_of_uranium*Scarcity_factor
	~	
	~		|

Final_energy_use_by_sector_and_type[ENERGY,SECTORS]=
	Desired_final_energy_by_sector_and_type[ENERGY,SECTORS]*Scarcity_factor
	~	
	~		|

Final_energy_use_and_non_energy_use_of_resources[ENERGY]=
	Desired_final_energy_resources_used_by_type[ENERGY]*Scarcity_factor
	~	
	~		|

Accumulated_depreciation_rate_caused_by_sea_level_rise_2°C= INTEG (
	Depreciation_rate_caused_by_sea_level_rise_2°C,
		0)
	~	
	~		|

Accumulated_depreciation_rate_caused_by_sea_level_rise_3°C= INTEG (
	Depreciation_rate_caused_by_sea_level_rise_3°C,
		0)
	~	
	~		|

Accumulated_depreciation_rate_caused_by_sea_level_rise_4°C= INTEG (
	Depreciation_rate_caused_by_sea_level_rise_4°C,
		0)
	~	
	~		|

Accumulated_extra_GFCF_due_to_sea_level_rise[SECTORS]= INTEG (
	Extra_GFCF_due_to_sea_level_rise[SECTORS],
		0)
	~	
	~		|

Primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS]=
	Desired_primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS]*Scarcity_factor
	~	
	~		|

Depreciation_by_sector[SECTORS]=
	Capital_stock[SECTORS]*(Depreciation_rate[SECTORS]+Depreciation_rate_caused_by_climate_change\
		[SECTORS]+Depreciation_rate_caused_by_sea_level_rise)
	~	
	~		|

CO2_from_fossil_energy_combustion=
	SUM(Final_energy_use_by_sector_and_type[FOSSIL_FUELS!,SECTORS!]*CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_FOSSIL_FUELS
	[FOSSIL_FUELS!]*FOSSIL_FUEL_EMISSIONS_INTENSITY[FOSSIL_FUELS!])
	~	MtCO2
	~	SUM(GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS!]*Output[SECTORS!]\
		)
	|

Threshold_of_3°C_exceeded=
	if_then_else(Year_threshold_of_3°C_exceeded=0,0,1)
	~	
	~		|

Threshold_of_4°C_exceeded=
	if_then_else(Year_threshold_of_4°C_exceeded=0,0,1)
	~	
	~		|

Heat_Transfer[Layer1]=
	(Temperature_change_base_1850-Relative_Deep_Ocean_Temp[Layer1])*Heat_Transfer_Coeff/\
		Mean_Depth_of_Adjacent_Layers
	[Layer1] ~~|
Heat_Transfer[lower]=
	(Relative_Deep_Ocean_Temp[upper]-Relative_Deep_Ocean_Temp[lower])
	*Heat_Transfer_Coeff/Mean_Depth_of_Adjacent_Layers[lower]
	~	watt/meter/meter
	~	Heat Transfer from the Atmosphere & Upper Ocean to the Deep Ocean
	|

Fossil_fuel_depletion=
	SUM(Primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS!])
	~	
	~		|

TOTAL_EXTRA_GFCF_DUE_TO_SEA_LEVEL_RISE_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'TOTAL_EXTRA_INVESTMENT_DUE_TO_SEA_LEVEL_RISE'\
		)
	~	
	~		|

Year_threshold_of_4°C_exceeded= INTEG (
	Flow_threshold_of_4°C_exceeded,
		0)
	~	
	~		|

Year_threshold_of_2°C_exceeded= INTEG (
	Flow_threshold_of_2°C_exceeded,
		0)
	~	
	~		|

Desired_final_energy_by_sector_and_type[ENERGY,SECTORS]=
	Desired_output_by_sector[SECTORS]*CONVERSION_FACTOR_MONETARY_TO_ENERGY[ENERGY,SECTORS\
		]
	~	
	~		|

Temperature_change_base_1750=
	Temperature_change_base_1850+0.1
	~	
	~	The IPCC also recognises that “both anthropogenic and natural changes to \
		the climate occurred” before the 1850-1900 baseline. For example, in its \
		2021 report on climate science, the IPCC estimates that between 1750 and \
		1850-1900, GMST increased by around 0.1C. Of this, human activity was \
		responsible for 0.0-0.2C, it says.
	|

Desired_non_energy_use_of_fossil_fuels[ENERGY]=
	SUM(Desired_output_by_sector[SECTORS!]*CONVERSION_FACTOR_MONETARY_TO_NON_ENERGY_USE_OF_FOSSIL_FUELS\
		[ENERGY,SECTORS!])
	~	
	~		|

MAXIMUM_SHARE_OF_EXTRACTABLE_FOSSIL_FUEL_RESOURCES_PER_YEAR_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Energy' , 'MAXIMUM_SHARE_OF_EXTRACTABLE_FOSSIL_FUEL_RESOURCES_PER_YEAR_SP'\
		)
	~	
	~		|

Threshold_of_2°C_exceeded=
	if_then_else(Year_threshold_of_2°C_exceeded=0,0,1)
	~	
	~		|

Desired_gross_fixed_capital_formation_by_sector[SECTORS]=
	SUM(Desired_investment_by_sector[SECTORS!])*Share_of_each_sector_in_gfcf[SECTORS]+Extra_GFCF_due_to_sea_level_rise\
		[SECTORS]
	~	million_euro/Year
	~	SUM(Desired_consumption_by_sector[SECTORS!])*SHARE_OF_EACH_SECTOR_IN_GROSS_FIXED_CAPI\
		TAL_FOMATION[SECTORS]*0.482848
		*prod(A_matrix_damage_factor[SECTORS!])
	|

Final_non_energy_use_fossil_fuels[ENERGY]=
	Desired_non_energy_use_of_fossil_fuels[ENERGY]*Scarcity_factor
	~	
	~		|

Temperature_change_base_1850=
	Heat_in_Atmosphere_and_Upper_Ocean/Atm_and_Upper_Ocean_Heat_Cap
	~	DegreesC
	~	Temperature of the Atmosphere and Upper Ocean, relative to preindustrial \
		reference period
	|

Year_threshold_of_3°C_exceeded= INTEG (
	Flow_threshold_of_3°C_exceeded,
		0)
	~	
	~		|

Feedback_Cooling=
	Temperature_change_base_1850*Climate_Feedback_Param
	~	watt/meter/meter
	~	Feedback cooling of atmosphere/upper ocean system due to blackbody \
		radiation. [Cowles, pg. 27]
	|

Final_demand_as_share_of_output=
	ZIDZ(Final_demand,Total_output)
	~	
	~		|

INITIAL_DISPOSABLE_LAND=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'DISPOSABLE_LAND'\
		)
	~	
	~		|

Disposable_land=
	INITIAL_DISPOSABLE_LAND-Land_loss_caused_by_climate_change-Foodland_loss_caused_by_climate_change
	~	
	~		|

MAXIMUM_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'MAXIMUM_LAND_LOSS_CAUSED_BY_CLIMATE_CHANGE'\
		)
	~	
	~		|

MAXIMUM_FOODLAND_LOSS_CAUSED_BY_CLIMATE_CHANGE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'MAXIMUM_FOODLAND_LOSS_CAUSED_BY_CLIMATE_CHANGE'\
		)
	~	
	~		|

Labour_demand[SECTORS]=
	Desired_output_by_sector[SECTORS]*Labour_intensity[SECTORS]*MATRIX_UNITS_PREFIXES[mega\
		,BASE_UNIT]
	~	
	~		|

SECTORAL_SHARES_OF_DAMAGES_IN_CAPITAL_STOCK_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'SECTORAL_SHARES_OF_DAMAGES_IN_CAPITAL_STOCK'\
		)
	~	
	~		|

OUTPUT_LOSSES_FACTOR_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'OUTPUT_LOSSES_FACTOR'\
		)
	~	
	~		|

ALPHA_DAMAGE_LABOUR_SUPPLY_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Labour' , 'ALPHA_DAMAGE_LABOUR_SUPPLY'\
		)
	~	
	~		|

ALPHA_DAMAGE_LABOUR_PRODUCTIVITY_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Labour' , 'ALPHA_DAMAGE_LABOUR_PRODUCTIVITY'\
		)
	~	
	~		|

MAXIMUM_PARTICIPATION_RATE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Labour' , 'MAXIMUM_PARTICIPATION_RATE_SP'\
		)
	~	
	~		|

Sectorial_land_demand[SECTORIAL_LANDS]=
	SUM(Desired_output_by_sector[SECTORS!]*Sectorial_land_intensities[SECTORIAL_LANDS,SECTORS\
		!])
	~	
	~		|

Depreciation_rate[SECTORS]=
	ZIDZ(INITIAL_DEPRECIATION_BY_SECTOR[SECTORS],Initial_capital_stock[SECTORS])
	~	
	~		|

FOSSIL_FUEL_EMISSIONS_INTENSITY[FOSSIL_FUELS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'FOSSIL_FUEL_EMISSIONS_INTENSITY*'\
		)
	~	
	~		|

Anthropogenic_CO2_Emissions_wo_LUC=
	Greenhouse_gas_emissions[CO2]+CO2_from_fossil_energy_combustion
	~	MtCO2/Year
	~		|

Anthropogenic_HFC_Emissions=
	Greenhouse_gas_emissions[HFC134a]
	~	tons/Year
	~	this is likely an overestimation due to the assumption that all HFCs are \
		HFC134a in exiobase  -> maybe apply a correction factor ? 797073
	|

Adjusted_Sensitivity_of_Sea_Level_Rise_to_Temperature=
	Sensitivity_of_Sea_Level_Rise_to_Temperature
	~	mm/(Year*DegreesC)
	~	a term could be added to reflect ice sheet melting
	|

Instant_Change_in_Sea_Level=
	Sensitivity_of_SLR_rate_to_temp_rate*Change_in_Relative_Temperature
	~	mm/Year
	~	Vermeer & Rahmstorf (2009) instantaneous sea level rise rate on the time \
		scales under consideration.  Rahmstorf (2007) is recovered when \
		Sensitivity of SLR rate to temp rate = W.
	|

Sea_Level_Rise= INTEG (
	Change_in_Sea_Level,
		initial_sea_level_rise_in_2019)
	~	mm
	~	IPCC: 4 degree: 0,7 m       however: 6,4 - 9,9 mm/year from 2040 onward
	|

Change_in_Sea_Level=
	Equilibrium_Change_in_Sea_Level+Instant_Change_in_Sea_Level
	~	mm/Year
	~		|

Adjusted_Temperature_change_from_preindustrial_for_SLR_estimation=
	Temperature_change_base_1850-Temp_Adjustment_for_SLR
	~	DegreesC
	~	Temperature change from preindustrial levels adjusted to the model \
		generated average global surface temperature that is used in the \
		calculation of sea level rise from the Vermeer and Rahmstorf (2009) model.
	|

Equilibrium_Change_in_Sea_Level=
	Adjusted_Sensitivity_of_Sea_Level_Rise_to_Temperature*(Adjusted_Temperature_change_from_preindustrial_for_SLR_estimation\
		-Reference_Temperature)
	~	mm/Year
	~	Vermeer & Rahmstorf (2009) sea level rise rate (open loop approx to \
		initial transient). Rahmstorf (2007) is recovered when Sensitivity of SLR \
		rate to temp rate = W.
	|

Change_in_Relative_Temperature=
	(Adjusted_Temperature_change_from_preindustrial_for_SLR_estimation-SMOOTH(Adjusted_Temperature_change_from_preindustrial_for_SLR_estimation\
		,TIME_STEP))/TIME_STEP
	~	DegreesC/Year
	~	approximates dT/dt
	|

Oceanic_pH_threshold=
	pH_constant_1-pH_constant_2*480+pH_constant_3*480^2-pH_constant_4*480^3
	~	pH
	~	Coral Reefs Under Rapid Climate Change and Ocean Acidification O. \
		Hoegh-Guldberg, et al. Science 318, 1737 (2007)
	|

pH_ocean=
	pH_constant_1-pH_constant_2*atmospheric_concentrations_CO2+pH_constant_3*atmospheric_concentrations_CO2\
		^2-pH_constant_4*atmospheric_concentrations_CO2^3
	~	pH
	~	pH of the ocean.
		Bernie, D., J. Lowe, T. Tyrrell, and O. Legge (2010), Influence of \
		mitigation policy on ocean acidification, Geophys. Res. Lett., 37, L15704, \
		doi:10.1029/2010GL043181.
	|

pH_in_2000=SAMPLE IF TRUE(
	Time<=2000, pH_ocean, pH_ocean)
	~	pH
	~		|

Delta_pH_from_2000=
	if_then_else(Time<2000, :NA:, pH_ocean-pH_in_2000)
	~	pH
	~	Change in pH from the pH in 2000.
	|

"2x_CO2_Forcing"= INITIAL(
	CO2_Rad_Force_coefficient*LN(2))
	~	watt/meter/meter
	~		|

sec_per_yr= INITIAL(
	DAYS_PER_YEAR*SECONDS_PER_YEAR)
	~	s/Year
	~	Converts seconds to years
	|

Deep_Ocean_Heat_Cap[Layers]= INITIAL(
	lower_layer_volume_Vu[Layers]*volumetric_heat_capacity/global_surface_area)
	~	watt*Year/(meter*meter)/DegreesC
	~	Volumetric heat capacity for the deep ocean by layer, i.e., lower layer \
		heat capacity Ru.
	|

Climate_Feedback_Param= INITIAL(
	"2x_CO2_Forcing"/Equilibrium_climate_sensitivity_SP)
	~	(watt/meter/meter)/DegreesC
	~	Climate Feedback Parameter - determines feedback effect from temperature \
		increase.
	|

Heat_Transfer_Coeff= INITIAL(
	(Heat_Transfer_Rate*Mean_Depth_of_Adjacent_Layers[Layer1])
	*(Heat_Diffusion_Covar*(Eddy_diff_coeff_0/Eddy_diff_mean)+(1-Heat_Diffusion_Covar)))
	~	watt/(meter*meter)/(DegreesC/meter) [0,1]
	~	The ratio of the actual to the mean of the heat transfer coefficient, \
		which controls the movement of heat through the climate sector, is a \
		function of the ratio of the actual to the mean of the eddy diffusion \
		coefficient, which controls the movement of carbon through the deep ocean.
	|

Equilibrium_climate_sensitivity_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Climate', 'Equilibrium_climate_sensitivity'\
		)
	~	DegreesC
	~	Equilibrium Climate Sensitivity.
	|

Eddy_diff_coeff_0= INITIAL(
	Eddy_diff_coeff_index*Eddy_diff_mean)
	~	meter*meter/Year
	~	Multiplier of eddy diffusion coefficient mean
	|

Heat_in_Atmosphere_and_Upper_Ocean= INTEG (
	Effective_Radiative_Forcing
	-Feedback_Cooling
	-Heat_Transfer[Layer1],
		init_Atmos_UOcean_Temp*Atm_and_Upper_Ocean_Heat_Cap)
	~	watt*Year/(meter*meter)
	~	Heat of the Atmosphere and Upper Ocean
	|

Atm_and_Upper_Ocean_Heat_Cap= INITIAL(
	upper_layer_volume_Vu*volumetric_heat_capacity/global_surface_area)
	~	watt*Year/(meter*meter)/DegreesC
	~	Volumetric heat capacity for the land, atmosphere,and upper ocean layer, \
		i.e., upper layer heat capacity Ru.
	|

lower_layer_volume_Vu[Layers]= INITIAL(
	global_surface_area*(1-land_area_fraction)*Layer_Depth[Layers])
	~	meter*meter*meter
	~	Water equivalent volume of the deep ocean by layer.
	|

Heat_in_Deep_Ocean[upper]= INTEG (
	Heat_Transfer[upper]-Heat_Transfer[lower],
		Init_Deep_Ocean_Temp[upper]*Deep_Ocean_Heat_Cap[upper]) ~~|
Heat_in_Deep_Ocean[bottom]= INTEG (
	Heat_Transfer[bottom],
		Init_Deep_Ocean_Temp[bottom]*Deep_Ocean_Heat_Cap[bottom])
	~	watt*Year/(meter*meter)
	~	Heat content of each layer of the deep ocean.
	|

Relative_Deep_Ocean_Temp[Layers]=
	Heat_in_Deep_Ocean[Layers]/Deep_Ocean_Heat_Cap[Layers]
	~	DegreesC
	~	Temperature of each layer of the deep ocean.
	|

volumetric_heat_capacity= INITIAL(
	SPECIFIC_HEAT_CAPACITY_WATER*WATT_PER_J_s/sec_per_yr*WATER_DENSITY)
	~	watt*Year/meter/meter/meter/DegreesC
	~	Volumetric heat capacity of water, i.e., amount of heat in watt*year \
		required to raise 1 cubic meter of water by one degree C.
	|

upper_layer_volume_Vu= INITIAL(
	global_surface_area*(land_area_fraction*land_thickness+(1-land_area_fraction)*Mixed_Depth\
		))
	~	meter*meter*meter
	~	Water equivalent volume of the upper box, which is a weighted combination \
		of land, atmosphere,and upper ocean volumes.
	|

Cumulative_GHG_emissions_GtCO2e= INTEG (
	Total_GHG_emissions_GtCO2e_wo_LUC,
		0)
	~	GTCO2e/Year
	~	Cumulative GHG emissions.
	|

Total_GHG_emissions_GtCO2e_wo_LUC=
	(Anthropogenic_CO2_Emissions_wo_LUC/1000)+
	Global_anthropogenic_CH4_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[CH4] , GWP_100_year
	[CH4])/MATRIX_UNIT_PREFIXES[giga,mega] +
	Anthropogenic_N2O_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[N2O\
		] , GWP_100_year
	[N2O])/MATRIX_UNIT_PREFIXES[giga,mega] +
	Anthropogenic_PFC_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[PFCs\
		] , GWP_100_year[PFCs]
	)/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_SF6_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[SF6] , GWP_100_year\
		[SF6])/
	MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC134a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC134a\
		] , GWP_100_year
	[HFC134a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC23]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC23\
		] , GWP_100_year
	[HFC23])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC32]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC32\
		] , GWP_100_year
	[HFC32])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC125]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC125\
		] , GWP_100_year
	[HFC125])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC143a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC143a\
		] , GWP_100_year
	[HFC143a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC152a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC152a\
		] , GWP_100_year
	[HFC152a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC227ea]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC227ea] , GWP_100_year
	[HFC227ea])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC245ca]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC245ca] , GWP_100_year
	[HFC245ca])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC4310mee]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[HFC4310mee] , GWP_100_year
	[HFC4310mee])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT]
	~	GTCO2e/Year
	~	Total greenhouse gas emissions from all sources except land use change
	|

Other_GHG_emissions[CH4]=
	Global_anthropogenic_CH4_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[CH4] , GWP_100_year[CH4])/MATRIX_UNIT_PREFIXES
	[giga,mega] ~~|
Other_GHG_emissions[N2O]=
	Anthropogenic_N2O_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[N2O\
		] , GWP_100_year
	[N2O])/MATRIX_UNIT_PREFIXES[giga,mega] ~~|
Other_GHG_emissions[PFCs]=
	Anthropogenic_PFC_Emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[PFCs\
		] , GWP_100_year[PFCs]
	)/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] ~~|
Other_GHG_emissions[SF6]=
	Global_SF6_emissions*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[SF6] , GWP_100_year\
		[SF6])/
	MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] ~~|
Other_GHG_emissions[HFC23]=
	Global_HFC_emissions[HFC134a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC134a\
		] , GWP_100_year
	[HFC134a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC23]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC23\
		] , GWP_100_year
	[HFC23])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC32]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC32\
		] , GWP_100_year
	[HFC32])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC125]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC125\
		] , GWP_100_year
	[HFC125])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC143a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC143a\
		] , GWP_100_year
	[HFC143a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC152a]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[HFC152a\
		] , GWP_100_year
	[HFC152a])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC227ea]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC227ea] , GWP_100_year
	[HFC227ea])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC245ca]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year[\
		HFC245ca] , GWP_100_year
	[HFC245ca])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT] +
	Global_HFC_emissions[HFC4310mee]*if_then_else(SWITCH_GWP_TIME_FRAME_SP=1, GWP_20_year\
		[HFC4310mee] , GWP_100_year
	[HFC4310mee])/MATRIX_UNIT_PREFIXES[giga,BASE_UNIT]
	~	GTCO2e/Year
	~	Other GHG emissions than CO2 by type of gas (in GtCO2e)
	|

SWITCH_GWP_TIME_FRAME_SP=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'SWITCH_GWP_TIME_FRAME_SP'\
		 )
	~	
	~	Choose GWP time frame:
		1: 20 years
		2: 100 years
	|

Total_cumulative_CO2_emissions_GtCO2= INTEG (
	(Anthropogenic_CO2_Emissions_wo_LUC/1000)+(Anthropogenic_LUC_CO2_Emissions/1000),
		Initial_cumulative_CO2_emissions)
	~	GtCO2
	~	Total cumulative CO2 emissions. Convert Anthropogenic CO2 emission in Gt
	|

Total_cumulative_C_emissions_GtC=
	Total_cumulative_CO2_emissions_GtCO2*C_PER_CO2
	~	GtC
	~	Total cumulative C emissions.
	|

Cumulative_GHG_emissions_GtCe=
	Cumulative_GHG_emissions_GtCO2e*C_PER_CO2
	~	GtC/Year
	~	Cumulative GHG emissions in carbon-content equivalent.
	|

CH4_Radiative_Forcing=
	CH4_radiative_efficiency_coefficient*(SQRT(CH4_atm_conc*CH4_N2O_unit_adj)
	-SQRT(CH4_reference_conc*CH4_N2O_unit_adj))
	-(Adjustment_for_CH4_and_N2Oref-Adjustment_for_CH4ref_and_N2Oref)
	~	watt/(meter*meter)
	~	AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table \
		8.SM.1 Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O.
	|

Stratospheric_water_vapour=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Stratospheric_water_vapour'\
		)
	~	watt/(meter*meter)
	~		|

Adjustment_for_CH4_and_N2Oref=
	CH4_N2O_interaction_coeffient * LN( 1
	+CH4_N2O_inter_coef_2 *(CH4_atm_conc*N2O_reference_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp
	+CH4_N2O_inter_coef_3 *CH4_atm_conc*CH4_N2O_unit_adj
	*(CH4_atm_conc*N2O_reference_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp_2)
	~	watt/(meter*meter)
	~	Part of the formula for calculating the radiative forcing from CH4 using \
		the N2O Reference Concentration. Source: "AR5 WG1 Chapter 8 Anthropogenic \
		and Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: \
		RF formulae for CO2, CH4 and N2O. Adjusts total RF from CH4 and N2O to be \
		less than  the sum of RF from each individually to account for \
		interactions  between both gases."
	|

Adjustment_for_CH4ref_and_N2O=
	CH4_N2O_interaction_coeffient * LN( 1
	+CH4_N2O_inter_coef_2 *(CH4_reference_conc*N2O_atm_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp
	+CH4_N2O_inter_coef_3 *CH4_reference_conc*CH4_N2O_unit_adj
	*(CH4_reference_conc*N2O_atm_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp_2)
	~	watt/(meter*meter)
	~	Part of the formula for calculating the radiative forcing from N2O using \
		the CH4 Reference Concentration. Source: "AR5 WG1 Chapter 8 Anthropogenic \
		and Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: \
		RF formulae for CO2,CH4 and N2O. Adjusts total RF from CH4 and N2O to be \
		less than  the sum of RF from each individually to account for \
		interactions  between both gases."
	|

Adjustment_for_CH4ref_and_N2Oref=
	CH4_N2O_interaction_coeffient * LN( 1
	+CH4_N2O_inter_coef_2 *(CH4_reference_conc*N2O_reference_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp
	+CH4_N2O_inter_coef_3 *CH4_reference_conc*CH4_N2O_unit_adj
	*(CH4_reference_conc*N2O_reference_conc
	*CH4_N2O_unit_adj*CH4_N2O_unit_adj)^CH4_N20_inter_exp_2)
	~	watt/(meter*meter)
	~	Parameter for calculating the radiative forcing from N2O and from CH4 \
		(both formulas) using the CH4 and N2O Reference Concentration. Source: \
		"AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table \
		8.SM.1 Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O. \
		Adjusts total RF from CH4 and N2O to be less than  the sum of RF from each \
		individually to account for interactions  between both gases."
	|

Aerosol_cloud_interactions=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Aerosol_cloud_interactions'\
		)
	~	watt/(meter*meter)
	~		|

Aerosol_radiation_interactions=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Aerosol_radiation_interactions'\
		)
	~	watt/(meter*meter)
	~		|

CO2e_ppm_concentrations=
	pre_industrial_ppm_CO2*EXP(ZIDZ( "Well-Mixed_GHG_Forcing" , CO2_Rad_Force_coefficient\
		 ))
	~	ppm
	~		|

Ozone=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Ozone')
	~	watt/(meter*meter)
	~		|

Contrails_and_aviation_induced_cirrus=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Contrails_and_aviation_induced_cirrus'\
		)
	~	
	~		|

RF_from_F_gases=
	PFC_RF+SF6_RF+HFC_RF_total
	~	watt/(meter*meter)
	~	Radiative forcing due to fluorinated gases, based on the concentration of \
		each gas multiplied by its radiative forcing coefficient.  The RF of HFCs \
		is the sum of the RFs of the individual HFC types:
	|

CH4_and_N2O_Radiative_Forcing=
	CH4_Radiative_Forcing + N2O_Radiative_Forcing
	~	watt/(meter*meter)
	~	AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table 8.SM.1 \
		Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O.
		Adjusts total RF from CH4 and N2O to be less than the sum of RF from each \
		individually to account for interactions between both gases.
	|

Effective_Radiative_Forcing=SAMPLE IF TRUE(
	Time<=Time_to_Commit_RF
	,Total_Radiative_Forcing,Total_Radiative_Forcing)
	~	watt/meter/meter
	~	Total Radiative Forcing from All GHGs
	|

"Other_GHG_Rad_Forcing_(non_CO2)"=
	Total_Radiative_Forcing-CO2_Radiative_Forcing
	~	
	~		|

N2O_Radiative_Forcing=
	N2O_radiative_efficiency_coefficient*(SQRT(N2O_atm_conc*CH4_N2O_unit_adj)
	-SQRT(N2O_reference_conc*CH4_N2O_unit_adj))
	-(Adjustment_for_CH4ref_and_N2O-Adjustment_for_CH4ref_and_N2Oref)
	~	watt/(meter*meter)
	~	AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table \
		8.SM.1 Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O.
	|

HFC_RF_total=
	SUM(HFC_RF[HFC_type!])
	~	watt/(meter*meter)
	~	The sum of the RFs of the individual HFC types.
	|

Land_use=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Land_use')
	~	watt/(meter*meter)
	~		|

Other_halocarbon=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Other_halocarbon'\
		)
	~	watt/(meter*meter)
	~		|

Total_Radiative_Forcing=
	"Well-Mixed_GHG_Forcing"+Other_Forcings
	~	watt/(meter*meter)
	~	problem. this is all for 1850. but ERF of IPCC is for 1750
	|

Other_Forcings=
	Aerosol_cloud_interactions+Aerosol_radiation_interactions+Contrails_and_aviation_induced_cirrus\
		+Land_use+Stratospheric_water_vapour+Ozone+Surface_albedo
	~	watt/(meter*meter)
	~	RCP does not include solar and albedo in their other forcings; the adjusted values \
		add the values for these from MAGICC. It is the adjusted other forcings \
		that are included in the total radiative forcing.
		+IF THEN ELSE(Time>=Last historical RF year, Mineral aerosols and land RF, \
		0)
	|

"Well-Mixed_GHG_Forcing"=
	CO2_Radiative_Forcing+CH4_and_N2O_Radiative_Forcing+Halocarbon_RF
	~	watt/(meter*meter)
	~		|

CO2_Radiative_Forcing=
	CO2_Rad_Force_coefficient*LN(C_in_Atmosphere/Preindustrial_C)
	~	watt/meter/meter
	~	Radiative forcing from accumulation of CO2.
		The ERF from doubling CO2 (2×CO2) from the 1750 level (278 ppm;
		Section 2.2.3.3) is assessed to be 3.93 ± 0.47 W m–2
	|

Halocarbon_RF=
	RF_from_F_gases+Other_halocarbon
	~	watt/(meter*meter)
	~	RF from PFCs, SF6, HFCs, and MP gases.
	|

Surface_albedo=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Surface_albedo'\
		)
	~	watt/(meter*meter)
	~		|

Initial_SF6=
	Initial_SF6_con/ppt_SF6_per_Tons_SF6
	~	tons
	~		|

CH4_Uptake_0=
	CH4_in_Atm_0*CH4_Fractional_Uptake_0
	~	Mtons/Year
	~	CH4 in Atm[regions]*CH4 Fractional Uptake[regions]
	|

ppt_PFC_per_Tons_PFC= INITIAL(
	ppt_PER_MOL/CF4_molar_mass*MATRIX_UNIT_PREFIXES[mega,BASE_UNIT])
	~	ppt/ton
	~	based on CF4
	|

ppt_SF6_per_Tons_SF6= INITIAL(
	ppt_PER_MOL/SF6_molar_mass*MATRIX_UNIT_PREFIXES[mega,BASE_UNIT])
	~	ppt/ton
	~		|

Initial_HFC[HFC_type]= INITIAL(
	Inital_HFC_con[HFC_type]/ppt_HFC_per_Tons_HFC[HFC_type])
	~	tons
	~		|

Init_PFC_in_Atm=
	Init_PFC_in_Atm_con/ppt_PFC_per_Tons_PFC
	~	tons
	~		|

SWITCH_RCP_POLICY_SP=
	3
	~	Dmnl
	~	Choose RCP (Representative Concentration Pathway)
		1. RCP 2.6
		2. RCP 4.5
		3. RCP 6.0
		4. RCP 8.5
	|

Anthropogenic_SF6_Emissions=
	Greenhouse_gas_emissions[SF6]
	~	tons/Year
	~		|

Global_SF6_emissions=
	Anthropogenic_SF6_Emissions
	~	tons/Year
	~	Historic data + projections "Representative Concentration Pathways" (RCPs, see \
		http://tntcat.iiasa.ac.at:8787/RcpDb/dsd?Action=htmlpage&page=compare)
		Choose RCP:
		1. RCP 2.6
		2. RCP 4.5
		3. RCP 6.0
		4. RCP 8.5
	|

CH4_atm_conc=
	CH4_in_Atm_0*ppb_CH4_per_Mton_CH4
	~	ppb
	~		|

Preindustrial_PFC= INITIAL(
	Preindustrial_PFC_conc/ppt_PFC_per_Tons_PFC)
	~	tons
	~		|

Anthropogenic_CH4_Emissions=
	Greenhouse_gas_emissions[CH4]
	~	MtCH4
	~	IPCC WG1 AR6: p.703: anthropogenic CH4 sources total (MtCH4): 350. \
		natural: 215 - 371
	|

Initial_CH4= INITIAL(
	Initial_CH4_conc/ppb_CH4_per_Mton_CH4)
	~	Mtons
	~		|

Time_Const_for_CH4=
	1/CH4_Fractional_Uptake_0
	~	Years [5,15]
	~		|

PFC_uptake=
	PFC_in_Atm/Time_Const_for_PFC
	~	tons/Year
	~		|

HFC_uptake[HFC_type]=
	HFC_in_Atm[HFC_type]/Time_Const_for_HFC[HFC_type]
	~	tons/Year
	~		|

N2O_Uptake=
	N2O_in_Atm/Time_Const_for_N2O
	~	Mton/Year
	~		|

Anthropogenic_N2O_Emissions=
	Greenhouse_gas_emissions[N2O]
	~	MtN/Year
	~	Mt N2O/year
	|

Anthropogenic_PFC_Emissions=
	Greenhouse_gas_emissions[PFCs]
	~	ton/Year
	~		|

SF6_in_Atm= INTEG (
	Global_SF6_emissions-SF6_uptake,
		Initial_SF6)
	~	tons
	~		|

N2O_in_Atm= INTEG (
	Global_N2O_Emissions-N2O_Uptake,
		Initial_N2O)
	~	Mtons_N [3.01279e-43,?]
	~		|

SF6_RF=
	(SF6_atm_conc-Preindustrial_SF6_conc)*SF6_radiative_efficiency/ppt_PER_ppb
	~	watt/(meter*meter)
	~	SF6 radiative forcing.
	|

Global_N2O_Emissions=
	Anthropogenic_N2O_Emissions+Natural_N2O_emissions
	~	Mton/Year
	~	Global N2O emissions.
	|

Global_total_PFC_emissions=
	Anthropogenic_PFC_Emissions+Natural_PFC_emissions
	~	tons/Year
	~	Global total PFC emissions
	|

PFC_in_Atm= INTEG (
	Global_total_PFC_emissions-PFC_uptake,
		Init_PFC_in_Atm)
	~	tons [3.01279e-43,?]
	~		|

ppt_HFC_per_Tons_HFC[HFC_type]= INITIAL(
	ppt_PER_MOL/HFC_molar_mass[HFC_type]*MATRIX_UNIT_PREFIXES[mega,BASE_UNIT])
	~	ppt/ton
	~		|

HFC_RF[HFC_type]=
	(HFC_atm_conc[HFC_type]-Preindustrial_HFC_conc)*HFC_radiative_efficiency[HFC_type]/ppt_PER_ppb
	~	watt/(meter*meter)
	~	HFC radiative forcing.
	|

CH4_Fractional_Uptake_0=
	1/Reference_CH4_time_constant*( Tropospheric_CH4_path_share/(Stratospheric_CH4_path_share\
		*(CH4_in_Atm_0/Preindustrial_CH4
	) + 1-Stratospheric_CH4_path_share) +(1-Tropospheric_CH4_path_share) )
	~	1/Years [5,15]
	~	dCH4/dt = E – k1*CH4*OH – k2*CH4
		E = emissions. The k1 path is dominant (k2 reflects soil processes and other minor \
		sinks)
		dOH/dt = F – k3*CH4*OH – k4*OH
		F = formation. In this case the methane reaction is the minor path (15-20% of loss) \
		so OH in equilibrium is
		OHeq = F/(k3*CH4+k4)
		substituting
		dCH4/dt = E – k1*CH4* F/(k3*CH4+k4) – k2*CH4
		thus the total fractional uptake is
		k1*F/(k3*CH4+k4)+k2
		which is robust at W
		Formulated from Meinshausen et al., 2011
	|

HFC_atm_conc[HFC_type]=
	HFC_in_Atm[HFC_type]*ppt_HFC_per_Tons_HFC[HFC_type]
	~	ppt
	~		|

CH4_in_Atm_0= INTEG (
	CH4_Emissions_from_Permafrost_and_Clathrate+Global_anthropogenic_CH4_emissions+Natural_CH4_Emissions\
		-CH4_Uptake_0,
		Initial_CH4)
	~	Mtons [3.01279e-43,?]
	~		|

SF6_atm_conc=
	SF6_in_Atm*ppt_SF6_per_Tons_SF6
	~	ppt
	~		|

Global_anthropogenic_CH4_emissions=
	Anthropogenic_CH4_Emissions
	~	MtCH4
	~	"Representative Concentration Pathways" (RCPs, see \
		http://tntcat.iiasa.ac.at:8787/RcpDb/dsd?Action=htmlpage&page=compare) \
		except  Power Plants, Energy Conversion, Extraction, and Distribution. \
		Corrected with endogenous data "Total CH4 emissions fossil fuels"
		Choose RCP:
	|

N2O_atm_conc=
	N2O_in_Atm*ppb_N2O_per_MTonN
	~	ppb
	~		|

HFC_in_Atm[HFC_type]= INTEG (
	Global_HFC_emissions[HFC_type]-HFC_uptake[HFC_type],
		Initial_HFC[HFC_type])
	~	tons [2.5924e-43,?]
	~		|

Global_CH4_emissions=
	Global_anthropogenic_CH4_emissions+Natural_CH4_Emissions
	~	Mtons/Year
	~	Global CH4 emission from anthropogenic and natural sources.
	|

PFC_atm_conc=
	PFC_in_Atm*ppt_PFC_per_Tons_PFC
	~	ppt
	~		|

ppb_N2O_per_MTonN= INITIAL(
	ppt_PER_MOL/N2O_N_molar_mass*MATRIX_UNIT_PREFIXES[mega,BASE_UNIT]*MATRIX_UNIT_PREFIXES\
		[mega,BASE_UNIT]/ppt_PER_ppb)
	~	ppb/Mton
	~		|

CH4_Emissions_from_Permafrost_and_Clathrate=
	SWITCH_Sensitivity_of_Methane_Emissions_to_Permafrost_and_Clathrate*Reference_Sensitivity_of_CH4_from_Permafrost_and_Clathrate_to_Temperature_SP
	*MAX(0,Temperature_change_base_1850-Temperature_Threshold_for_Methane_Emissions_from_Permafrost_and_Clathrate_SP
	)
	~	MtCH4
	~	Methane emissions from melting permafrost and clathrate outgassing are \
		assumed to be nonlinear. Emissions are assumed to be zero if warming over \
		preindustrial levels is less than a threshold and linear in temperature \
		above the threshold. The default sensitivity is zero, but the strength of \
		the effect and threshold can be set by the user.
	|

PFC_RF=
	(PFC_atm_conc-Preindustrial_PFC_conc)*PFC_radiative_efficiency/ppt_PER_ppb
	~	watt/(meter*meter)
	~	PFC radiative forcing.
	|

SF6_uptake=
	SF6_in_Atm/Time_Const_for_SF6
	~	tons/Year
	~		|

ppb_CH4_per_Mton_CH4= INITIAL(
	ppt_PER_MOL/CH4_molar_mass*MATRIX_UNIT_PREFIXES[mega,BASE_UNIT]*MATRIX_UNIT_PREFIXES\
		[mega,BASE_UNIT]/ppt_PER_ppb)
	~	ppb/Mton
	~		|

Total_CH4_released= INTEG (
	CH4_Emissions_from_Permafrost_and_Clathrate/CH4_PER_C/MATRIX_UNIT_PREFIXES[giga,mega\
		],
		0)
	~	GtonsC
	~	Of C emissions released from melting of permafrost, only about 2.3 % was \
		expected to be in the form of CH4, corresponding to W.26-0.85 Pg CH4-C by \
		2040, 2.03-6.21 Pg CH4-C by 2100 and 4.61-14.24 Pg CH4-C by 2300 (Fig. 1d).
	|

Initial_N2O= INITIAL(
	Initial_N2O_conc/ppb_N2O_per_MTonN)
	~	Mtons_N
	~		|

Total_C_from_permafrost= INTEG (
	Flux_C_from_permafrost_thaw+CH4_Emissions_from_Permafrost_and_Clathrate/CH4_PER_C/MATRIX_UNIT_PREFIXES\
		[giga,mega],
		0)
	~	GtonsC
	~	In terms of total C mass (of both CO2 and CH4) released from permafrost \
		melting, experts estimated that 15-33 Pg C (n=27) could be released by \
		2040, reaching 120-195 Pg C by 2100, and 276-414 Pg C by 2300 under the \
		high warming scenario (Fig. 1c). 1 PgC = 1GtonC.
	|

init_C_in_atmosphere=
	init_CO2_in_atmosphere_ppm*GtC_PER_ppm
	~	GtC [500,1000]
	~	Initial C in atmosphere.
		
		[DICE-1994] Initial Greenhouse Gases in Atmosphere 1965 [M(t)] (tC equivalent). \
		[Cowles, pg. 21] /6.77e+011 /
		[DICE-2013R] mat0: Initial concentration in atmosphere 2010 (GtC) /830.4 /
	|

C_in_Humus= INTEG (Flux_Biomass_to_Humus-Flux_Humus_to_Atmosphere-Flux_Humus_to_CH4,
		Init_C_in_Humus)
	~	GtC
	~	Carbon in humus.
	|

Preind_C_in_Mixed_Layer= INITIAL(
	Preind_Ocean_C_per_meter*Mixed_Depth)
	~	GtC
	~	Initial carbon concentration of mixed ocean layer.
	|

C_in_mixed_layer_per_meter=
	C_in_Mixed_Layer/Mixed_Depth
	~	GtC/meter
	~		|

C_in_permafrost= INTEG (
	-Flux_C_from_permafrost_thaw,
		Initial_C_in_permafrost)
	~	GtC
	~		|

Flux_Biomass_to_Humus=
	C_in_Biomass/Biomass_Res_Time*Humification_Fraction
	~	GtC/Year
	~	Carbon flux from biomass to humus.
	|

Flux_Biosphere_to_CH4=
	Flux_Biomass_to_CH4+Flux_Humus_to_CH4
	~	GtC/Year
	~	Carbon flux from biosphere as methane, in GtC/year, arising from anaerobic \
		respiration.
	|

Flux_C_from_permafrost_thaw=
	SWITCH_Sensitivity_of_Methane_Emissions_to_Permafrost_and_Clathrate*Reference_Sensitivity_of_C_from_Permafrost_and_Clathrate_to_Temperature_SP
	*MAX(0,Temperature_change_base_1850-Temperature_Threshold_for_Methane_Emissions_from_Permafrost_and_Clathrate_SP
	)
	~	GtC/Year
	~		|

Flux_Humus_to_Atmosphere=
	C_in_Humus/Humus_Res_Time
	~	GtC/Year
	~	Carbon flux from humus to atmosphere.
	|

Flux_Humus_to_CH4=
	C_in_Humus*CH4_Generation_Rate_from_Humus*Effect_of_Warming_on_CH4_Release_from_Biological_Activity
	~	GtC/Year
	~	The natural flux of methane from C in humus. The sum of the flux of \
		methane from C in humus and the flux of methane from C in biomass yields \
		the natural emissions of methane. Adjusted to account for temperature \
		feedback.
	|

CH4_Fractional_Uptake=
	1/Reference_CH4_time_constant*( Tropospheric_CH4_path_share/(Stratospheric_CH4_path_share\
		*(CH4_in_Atm/Preindustrial_CH4
	) + 1-Stratospheric_CH4_path_share) +(1-Tropospheric_CH4_path_share) )
	~	1/Years
	~	dCH4/dt = E – k1*CH4*OH – k2*CH4
		E = emissions. The k1 path is dominant (k2 reflects soil processes and other minor \
		sinks)
		dOH/dt = F – k3*CH4*OH – k4*OH
		F = formation. In this case the methane reaction is the minor path (15-20% of loss) \
		so OH in equilibrium is
		OHeq = F/(k3*CH4+k4)
		substituting
		dCH4/dt = E – k1*CH4* F/(k3*CH4+k4) – k2*CH4
		thus the total fractional uptake is
		k1*F/(k3*CH4+k4)+k2
		which is robust at W
		Formulated from Meinshausen et al., 2011
	|

Initial_C_in_permafrost=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'C_in_permafrost'\
		)
	~	GtC
	~		|

Anthropogenic_C_combustion=
	(Anthropogenic_CO2_Emissions_wo_LUC/1000)*C_PER_CO2
	~	GtC
	~		|

Anthropogenic_C_combustion_0=
	(Anthropogenic_CO2_Emissions_wo_LUC/1000)*C_PER_CO2
	~	GtC
	~		|

Anthropogenic_LUC_CO2_Emissions=
	SUM(Land_use_change_emissions_by_land[LAND_EMISSIONS!])
	~	MtCO2/Year
	~		|

atmospheric_concentrations_CO2=
	C_in_Atmosphere / GtC_PER_ppm
	~	ppm
	~	C_in_Atmosphere / GtC_per_ppm
		
		1 part per million of atmospheric CO2 is equivalent to 2.13 Gigatonnes Carbon.
		
		Historical Mauna Loa CO2 Record: \
		ftp://ftp.cmdl.noaa.gov/products/trends/co2/co2_mm_mlo.txt
	|

Equil_C_in_Mixed_Layer=
	Preind_C_in_Mixed_Layer*Effect_of_Temp_on_DIC_pCO2*(C_in_Atmosphere/Preindustrial_C)\
		^(1/Buffer_Factor)
	~	GtC
	~	Equilibrium carbon content of mixed layer.  Determined by the Revelle buffering \
		factor, and by temperature.  For simplicity, we assume a linear impact of \
		warming on the equilibrium solubility of CO2 in the ocean.
		10*0,985*3^(1/719,6) buffer
	|

bottom:
	Layer4
	~	
	~		|

Equilibrium_C_per_meter_in_Mixed_Layer=
	Equil_C_in_Mixed_Layer/Mixed_Depth
	~	GtC/meter
	~	The equilibrium concentration of C in the mixed layer, in GtC/meter, based \
		on the total quantity of C in that layer and the average layer depth.
	|

Reference_Sensitivity_of_C_from_Permafrost_and_Clathrate_to_Temperature_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Climate', 'Reference_Sensitivity_of_C_from_Permafrost_and_Clathrate_to_Temperature'\
		)
	~	GtonsC/(Year*DegreeC)
	~		|

Fossil_Resources= INTEG (
	-Anthropogenic_C_combustion_0,
		Coal_Resources+Gas_Resources+Oil_Resources)
	~	GtC
	~	includes carbon, oil and gas
	|

Gas_Reserves=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Gas_Reserves'\
		)
	~	GtC
	~		|

Gas_Resources=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Gas_Resources'\
		)
	~	GtC
	~		|

CH4_Uptake=
	CH4_in_Atm*CH4_Fractional_Uptake
	~	Mtons/Year
	~	CH4 in Atm[regions]*CH4 Fractional Uptake[regions]
	|

Natural_CH4_Emissions=
	Flux_Biosphere_to_CH4*CH4_PER_C*MATRIX_UNIT_PREFIXES[giga,mega]
	~	MtCH4
	~	Flux of methane from anaerobic respiration in the biosphere, in Mtons \
		CH4/year.
	|

Flux_Atm_to_Biomass=
	Init_NPP* (1+ Biostimulation_coeff* LN(C_in_Atmosphere/Preindustrial_C))*Effect_of_Warming_on_C_flux_to_biomass
	~	GtC/Year
	~	Carbon flux from atmosphere to biosphere (from primary production)
	|

Coal_Reserves=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Coal_Reserves'\
		)
	~	GtC
	~		|

Coal_Resources=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Coal_Resources'\
		)
	~	GtC
	~		|

Flux_Biomass_to_CH4=
	C_in_Biomass*CH4_Generation_Rate_from_Biomass*Effect_of_Warming_on_CH4_Release_from_Biological_Activity
	~	GtC/Year
	~	The natural flux of methane from C in biomass. The sum of the flux of \
		methane from C in humus and the flux of methane from C in biomass yields \
		the natural emissions of methane.  Adjusted to account for temperature \
		feedback.
	|

Diffusion_Flux[Layer1]=
	(C_in_mixed_layer_per_meter-C_in_deep_ocean_per_meter[Layer1])*Eddy_diff_coeff/Mean_Depth_of_Adjacent_Layers\
		[Layer1] ~~|
Diffusion_Flux[lower]=
	(C_in_deep_ocean_per_meter[upper]
	-C_in_deep_ocean_per_meter[lower])
	*Eddy_diff_coeff/Mean_Depth_of_Adjacent_Layers[lower]
	~	GtC/Year
	~	Diffusion flux between ocean layers.
	|

Biostimulation_coeff= INITIAL(
	Biostimulation_coeff_index*Biostimulation_coeff_mean)
	~	Dmnl
	~	Coefficient for response of primary production to carbon concentration.
	|

Oil_Resources=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Oil_Resources'\
		)
	~	GtC
	~		|

Eddy_diff_coeff= INITIAL(
	Eddy_diff_coeff_index*Eddy_diff_mean)
	~	meter*meter/Year
	~	Multiplier of eddy diffusion coefficient mean
	|

C_in_Biomass= INTEG (
	Flux_Atm_to_Biomass-Flux_Biomass_to_Atmosphere-Flux_Biomass_to_CH4-Flux_Biomass_to_Humus\
		,
		Init_C_in_Biomass)
	~	GtC
	~	Carbon in biomass.
	|

Effect_of_Temp_on_DIC_pCO2=
	1-Sensitivity_of_pCO2_DIC_to_Temperature*Temperature_change_base_1850
	~	Dmnl
	~	The fractional reduction in the solubility of CO2 in ocean falls with \
		rising temperatures.  We assume a linear relationship, likely a good \
		approximation over the typical range for warming by 2100.
	|

Effect_of_Warming_on_C_flux_to_biomass=
	1+Strength_of_Temp_Effect_on_C_Flux_to_Land*Temperature_change_base_1850
	~	Dmnl
	~	The fractional reduction in the flux of C from the atmosphere to biomass \
		with rising temperatures.  We assume a linear relationship, likely a good \
		approxim
	|

Effect_of_Warming_on_CH4_Release_from_Biological_Activity=
	1+SWITCH_Sensitivity_of_Methane_Emissions_to_Temperature*(Temperature_change_base_1850\
		)/(Reference_Temperature_Change_for_Effect_of_Warming_on_CH4_from_Respiration
	)
	~	Dmnl
	~	The fractional increase in the flux of C as CH4 from humus with rising \
		temperatures. We assume a linear relationship, likely a good approximation \
		over the typical range for warming by 2100.
	|

Mean_Depth_of_Adjacent_Layers[Layer1]= INITIAL(
	(Mixed_Depth+Layer_Depth[Layer1])/2) ~~|
Mean_Depth_of_Adjacent_Layers[lower]=
	(Layer_Depth[upper]+Layer_Depth[lower])/2
	~	meter
	~	The mean depth of adjacent ocean layers.
	|

Flux_Biomass_to_Atmosphere=
	C_in_Biomass/Biomass_Res_Time*(1-Humification_Fraction)+(Anthropogenic_LUC_CO2_Emissions\
		/1000)
	~	GtC/Year
	~	Carbon flux from biomass to atmosphere.
	|

upper:
	(Layer1-Layer3) -> lower
	~	
	~		|

lower:
	(Layer2-Layer4) -> upper
	~	
	~		|

C_in_deep_ocean_per_meter[Layers]=
	C_in_Deep_Ocean[Layers]/Layer_Depth[Layers]
	~	GtC/meter
	~	Concentration of carbon in ocean layers.
	|

Buffer_Factor= ACTIVE INITIAL (
	Ref_Buffer_Factor*(C_in_Mixed_Layer/Preind_C_in_Mixed_Layer)^Buff_C_Coeff
	,
		Ref_Buffer_Factor)
	~	Dmnl
	~	Buffer factor for atmosphere/mixed ocean carbon equilibration.9,7*3^3,92 \
		=719,6
	|

C_from_CH4_oxidation=
	CH4_Uptake/CH4_PER_C/MATRIX_UNIT_PREFIXES[giga,mega]
	~	GtonsC/Year
	~	Flux of C into the atmosphere from the oxidation of CH4, the mode of \
		removal of CH4 from atmosphere.
	|

C_in_Atmosphere= INTEG (
	Anthropogenic_C_combustion+C_from_CH4_oxidation+Flux_Biomass_to_Atmosphere+Flux_C_from_permafrost_thaw\
		+Flux_Humus_to_Atmosphere-Flux_Atm_to_Biomass-Flux_Atm_to_Ocean,
		init_C_in_atmosphere)
	~	GtC
	~	Carbon  in atmosphere.
	|

Strength_of_Temp_Effect_on_C_Flux_to_Land= INITIAL(
	SWITCH_Sensitivity_of_C_Uptake_to_Temperature*Strength_of_temp_effect_on_land_C_flux_mean\
		)
	~	1/DegreesC
	~	Strength of temperature effect on C flux to the land.
	|

C_in_Deep_Ocean[upper]= INTEG (
	Diffusion_Flux[upper]-Diffusion_Flux[lower],
		Init_C_in_Deep_Ocean_per_meter[upper]*Layer_Depth[upper]) ~~|
C_in_Deep_Ocean[bottom]= INTEG (
	Diffusion_Flux[bottom],
		Init_C_in_Deep_Ocean_per_meter[bottom]*Layer_Depth[bottom])
	~	GtC
	~	Carbon in deep ocean.
	|

Flux_Atm_to_Ocean=
	((Equil_C_in_Mixed_Layer-C_in_Mixed_Layer)/Mixing_Time)
	~	GtC/Year
	~	Carbon flux from atmosphere to mixed ocean layer.
	|

Oil_Reserves=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Oil_Reserves'\
		)
	~	GtC
	~		|

C_in_Mixed_Layer= INTEG (
	Flux_Atm_to_Ocean-Diffusion_Flux[Layer1],
		Init_C_in_Mixed_Ocean_per_meter*Mixed_Depth)
	~	GtC
	~	Carbon in mixed layer.
	|

GtC_PER_ppm=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'GtC_PER_ppm')
	~	GtC/ppm
	~		|

CH4_in_Atm= INTEG (
	CH4_Emissions_from_Permafrost_and_Clathrate+Global_anthropogenic_CH4_emissions+Natural_CH4_Emissions\
		-CH4_Uptake_0,
		Initial_CH4)
	~	Mtons
	~		|

Layer_Time_Constant[Layer1]= INITIAL(
	Layer_Depth[Layer1]/(Eddy_diff_coeff/Mean_Depth_of_Adjacent_Layers[Layer1])) ~~|
Layer_Time_Constant[lower]= INITIAL(
	Layer_Depth[lower]/(Eddy_diff_coeff/Mean_Depth_of_Adjacent_Layers[lower]))
	~	Year
	~	Time constant of exchange between layers.
	|

Fossil_Reserves= INTEG (
	-Anthropogenic_C_combustion,
		Coal_Reserves+Gas_Reserves+Oil_Reserves)
	~	GtC
	~	includes coal, oil and gas
	|

Sensitivity_of_pCO2_DIC_to_Temperature= INITIAL(
	SWITCH_Sensitivity_of_C_Uptake_to_Temperature*Sensitivity_of_pCO2_DIC_to_Temperature_Mean\
		)
	~	1/DegreesC
	~	Sensitivity of pCO2 of dissolved inorganic carbon in ocean to temperature.
	|

MATRIX_UNIT_PREFIXES[unit_prefixes,unit_prefixes_1]=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'Constants', 'Prefix_units'\
		)
	~	Dmnl
	~	Conversion from Matrix unit prefixes[tera,BASE UNIT] (1 T$ = 1e12 $). -> \
		da wird ne ganze matrix importiert und zwar eine quadratische, wo die \
		reihen den spalten entsprechen
	|

INITIAL_SIMULATION_YEAR=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'initial_simulation_year'\
		)
	~	Year
	~	Initial simulation year.
	|

ppt_PER_MOL==
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'Constants', 'ppt_per_mol')
	~	ppt/mol
	~	Parts per trillion per mol.
	|

ppt_PER_ppb==
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'Constants', 'ppt_per_ppb')
	~	ppt/ppb
	~	Parts-per-trillion per parts-per-billion.
	|

WATT_PER_J_s=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'watt_per_J_s'\
		)
	~	watt/(J/s)
	~	Converts watts to J/s.
	|

WATER_DENSITY=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'water_density'\
		)
	~	kg/meter/meter/meter
	~	Density of water, i.e., mass per volume of water.
	|

C_PER_CO2=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'C_PER_CO2')
	~	gC/gCO2e
	~	1 g of CO2 contains 3/11 of carbon.
	|

DAYS_PER_YEAR=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'days_per_year'\
		)
	~	days/Year
	~	Constant: 365 days in a year.  ##'constants' ist wohl der sheet name; \
		'days per year' ist der name der zelle (B42)
	|

SECONDS_PER_YEAR=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'seconds_per_day'\
		)
	~	s/day
	~	86400 (60*60*24) seconds per day
	|

CH4_PER_C==
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'CH4_per_C')
	~	gCH4/gC
	~	Molar mass ratio of CH4 to C, 16/12
	|

SPECIFIC_HEAT_CAPACITY_WATER=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'constants', 'specific_heat_capacity_water'\
		)
	~	J/kg/DegreesC
	~	Specific heat of water, i.e., amount of heat in Joules per kg water \
		required to raise the temperature by one degree Celsius.
	|

PERCENT_TO_SHARE=
	GET_DIRECT_CONSTANTS('/model_parameters/constants.xlsx', 'Constants', 'percent_to_share'\
		)
	~	Dmnl
	~	Conversion of percent to share.
	|

Preindustrial_SF6_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Preindustrial_SF6_conc'\
		)
	~	ppt
	~		|

Initial_CH4_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Initial_CH4_conc'\
		)
	~	ppb
	~	Historical data. NASA. GISS. https://data.giss.nasa.gov/modelforce/ghgases/
	|

CH4_Generation_Rate_from_Humus=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_Generation_Rate_from_Humus'\
		)
	~	1/Year [0,0.00016]
	~	The rate of the natural flux of methane from C in humus. The sum of the \
		flux of methane from C in humus and the flux of methane from C in biomass \
		yields the natural emissions of methane.
	|

Initial_cumulative_CO2_emissions=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Cumulative_CO2_emissions_1850_2018'\
		)
	~	GtCO2
	~	Cumulative CO2 emissions 1850-2018 (including 2018) due to fossil fuel \
		combustion, cement production and land-use changes.
	|

CH4_N20_inter_exp=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N20_inter_exp'\
		)
	~	Dmnl
	~	First exponent of CH4 N2O interaction. AR5 WG1 Chapter 8 Anthropogenic and \
		Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: RF \
		formulae for CO2, CH4 and N2O.
	|

CH4_N20_inter_exp_2=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N20_inter_exp_2'\
		)
	~	Dmnl
	~	Second exponent of CH4 N2O interaction. AR5 WG1 Chapter 8 Anthropogenic \
		and Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: \
		RF formulae for CO2, CH4 and N2O.
	|

Initial_N2O_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Initial_N2O_conc'\
		)
	~	ppb
	~	Historical data. NASA. GISS. https://data.giss.nasa.gov/modelforce/ghgases/
	|

CH4_N2O_inter_coef_3=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N2O_inter_coef_3'\
		)
	~	Dmnl
	~	Coefficient of CH4 N2O interaction. AR5 WG1 Chapter 8 Anthropogenic and \
		Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: RF \
		formulae for CO2, CH4 and N2O.
	|

CH4_N2O_interaction_coeffient=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N2O_interaction_coeffient'\
		)
	~	watt/(meter*meter)
	~	Coefficient of CH4 N2O interaction. AR5 WG1 Chapter 8 Anthropogenic and \
		Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: RF \
		formulae for CO2, CH4 and N2O.
	|

CH4_N2O_unit_adj==
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N2O_unit_adj'\
		)
	~	1/ppb
	~	Normalizes units to avoid dimensioned variable in exponent
	|

Ref_Buffer_Factor=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Ref_Buffer_Factor'\
		)
	~	Dmnl
	~	Normal buffer factor.
	|

initial_sea_level_rise_in_2019=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'initial_SLR_2019'\
		 )
	~	mm [-400,400]
	~	Estimated SLR in 1995.
	|

Reference_Sensitivity_of_CH4_from_Permafrost_and_Clathrate_to_Temperature_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Climate', 'Reference_Sensitivity_of_CH4_from_Permafrost_and_Clathrate_to_Temperature'\
		)
	~	Mtons/Year/DegreeC
	~	The reference emissions of methane from melting permafrost and outgassing \
		from clathrates per degree C of warming above the threshold.
	|

Initial_SF6_con=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Initial_SF6_con'\
		)
	~	ppt
	~	Historical data. NASA. GISS. https://data.giss.nasa.gov/modelforce/ghgases/
	|

Reference_Temperature_Change_for_Effect_of_Warming_on_CH4_from_Respiration=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Reference_Temperature_Change_for_Effect_of_Warming_on_CH4_from_Respiration'\
		)
	~	DegreesC
	~	Temperature change at which the C as CH4 release from humus doubles for \
		the Sensitivity of Methane Emissions to Temperature=1.
	|

N2O_reference_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'N2O_reference_conc'\
		)
	~	ppb
	~	WG1AR5_Chapter08_FINAL.pdf.  \
		https://www.ipcc.ch/pdf/assessment-report/ar5/wg1/WG1AR5_Chapter08_FINAL.pd\
		f
	|

Natural_N2O_emissions=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Natural_N2O_emissions'\
		)
	~	MtonN/Year [0,20]
	~	AR5 WG1 Chapter 6 Table 6.9
	|

Heat_Transfer_Rate=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Heat_Transfer_Rate'\
		)
	~	watt/(meter*meter)/DegreesC [0,2]
	~		|

HFC_molar_mass[HFC_type]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'HFC_molar_mass*'\
		)
	~	g/mole
	~	http://www.qc.ec.gc.ca/dpe/publication/enjeux_ges/hfc134a_a.html
	|

HFC_radiative_efficiency[HFC_type]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'HFC_radiative_efficiency*'\
		)
	~	watt/(ppb*meter*meter)
	~	From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

land_area_fraction=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'land_area_fraction'\
		)
	~	fraction
	~	Fraction of global surface area that is land.
	|

Humification_Fraction=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Humification_Fraction'\
		)
	~	Dmnl
	~	Fraction of carbon outflow from biomass that enters humus stock.
	|

Humus_Res_Time=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Humus_Res_Time'\
		)
	~	Year
	~	Average carbon residence time in humus.
	|

CH4_molar_mass==
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_molar_mass'\
		)
	~	g/mole
	~	Molar mass of CH4.
	|

Eddy_diff_coeff_index=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Eddy_diff_coeff_index'\
		)
	~	Dmnl [0.85,1.15]
	~	Index of coefficient for rate at which carbon is mixed in the ocean due to \
		eddy motion, where 1 is equivalent to the expected value (defaulted to \
		4400 meter*meter/year).
	|

Biomass_Res_Time=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Biomass_Res_Time'\
		)
	~	Year
	~	Average residence time of carbon in biomass.
	|

Biostimulation_coeff_index=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Biostim_coeff_index'\
		)
	~	Dmnl [0.6,1.7]
	~	Index of coefficient for response of primary production to carbon \
		concentration, as multiplying factor of the mean value.
	|

Biostimulation_coeff_mean=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Biostim_coeff_mean'\
		)
	~	Dmnl [0.3,0.7]
	~	Mean coefficient for response of primary production to CO2 concentration. Reflects \
		the increase in NPP with doubling the CO2 level.
		Goudriaan and Ketner, 1984; Rotmans, 1990
	|

Sensitivity_of_Sea_Level_Rise_to_Temperature=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'Sensitivity_of_Sea_Level_Rise_to_Temperature'\
		 )
	~	(mm/Year)/DegreesC
	~	Sensitivity of sea level rise to temperature anomaly.  From V&R (2009) \
		supplement, table S1. Rahmstorf (2007) uses 3.4
	|

Sensitivity_of_SLR_rate_to_temp_rate=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'Sensitivity_of_SLR_rate_to_temp_rate'\
		 )
	~	mm/DegreesC [-100,100]
	~	Slope of instantaneous temperature change - sea level change relationship \
		(Vermeer & Rahmstorf, 2009) From V&R (2009) supplement, table S1. \
		Rahmstorf (2007) uses W (i.e. term is missing)
	|

SF6_molar_mass==
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'SF6_molar_mass'\
		)
	~	g/mole
	~		|

Layer_Depth[Layers]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Layer_Depth_Layers*'\
		)
	~	meter
	~	Deep ocean layer thicknesses.
	|

Layers:
	(Layer1-Layer4)
	~	
	~	Deep ocean layers.
	|

Init_C_in_Mixed_Ocean_per_meter=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_C_in_Mixed_Ocean_per_meter'\
		)
	~	GtC/meter
	~	Initial carbon in mixed ocean layer.
	|

init_CO2_in_atmosphere_ppm=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'init_CO2_in_Atmos_ppm'\
		)
	~	ppm
	~	Initial CO2 in atmosphere.
		Historical Mauna Loa CO2 Record: Average between 1st and last month of 1990 was: \
		(353.74+355.12)/2=354.43 ppm
		Historical Mauna Loa CO2 Record: Average between 1st and last month of 1995 was: \
		(359.92+360.68)/2= 360.3 ppm
		ftp://ftp.cmdl.noaa.gov/products/trends/co2/co2_mm_mlo.txt
		
		[DICE-1994] Initial Greenhouse Gases in Atmosphere 1965 [M(t)] (tC equivalent). \
		[Cowles, pg. 21] /6.77e+011 /
		[DICE-2013R] mat0: Initial concentration in atmosphere 2010 (GtC) /830.4 /
	|

pre_industrial_ppm_CO2=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'pre_industrial_value_ppm'\
		)
	~	ppm
	~	Pre-industrial CO2 concentrations (275 ppm).
	|

Buff_C_Coeff=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Buff_C_Coeff'\
		)
	~	Dmnl
	~	Coefficient of CO2 concentration influence on buffer factor.
	|

Strength_of_temp_effect_on_land_C_flux_mean=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Strength_of_temp_effect_on_land_C_flux_mean'\
		)
	~	1/DegreesC
	~	Average effect of temperature on flux of carbon to land. Calibrated to be \
		consistent with Friedlingstein et al., 2006.  Climate-Carbon Cycle \
		Feedback Analysis: ResuMCS from the C4MIP Model Intercomparison.  Journal \
		of Climate. p3337-3353.  Default Sensitivity of C Uptake to Temperature of \
		1 corresponds to mean value from the 11 models tested.
	|

Preindustrial_CH4=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Preindustrial_CH4'\
		)
	~	Mtons
	~	Law Dome ice core
	|

Preindustrial_HFC_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Preindustrial_HFC_conc'\
		)
	~	ppt
	~		|

CF4_molar_mass==
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CF4_molar_mass'\
		)
	~	g/mole
	~		|

CH4_Generation_Rate_from_Biomass=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_Generation_Rate_from_Biomass'\
		)
	~	1/Year [0,0.00014]
	~	The rate of the natural flux of methane from C in biomass. The sum of the \
		flux of methane from C in humus and the flux of methane from C in biomass \
		yields the natural emissions of methane.
	|

Reference_CH4_time_constant=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Reference_CH4_time_constant'\
		)
	~	Year [8,10]
	~	Calculated from AR5 WG1 Chapter 6
	|

CO2_Rad_Force_coefficient=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CO2_Rad_Force_C_ROADS'\
		)
	~	watt/meter/meter
	~	Coefficient of Radiative Forcing from CO2
		From IPCC
	|

Temp_Adjustment_for_SLR=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'Temp_adjustment_for_SLR'\
		 )
	~	DegreesC
	~	Adjustment to global surface temperature that is relative to \
		pre-industrial levels from the average of the 1951-1980 data that Vermeer \
		and Rahmstorf (2009) used based on GISTEMP. See V&R 2009 supplement.
	|

Temperature_Threshold_for_Methane_Emissions_from_Permafrost_and_Clathrate_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Climate', 'Temperature_Threshold_for_Methane_Emissions_from_Permafrost_and_Clathrate'\
		)
	~	DegreesC [0,4]
	~	The threshold rise in global mean surface temperature above preindustrial \
		levels that triggers the release of methane from permafrost and \
		clathrates. Below this threshold, emissions from	these sources are assumed \
		to be zero. Above the threshold, emissions are assumed to rise linearly \
		with temperature.
	|

CH4_N2O_inter_coef_2=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_N2O_inter_coef_2'\
		)
	~	Dmnl
	~	Coefficient of CH4 N2O interaction. AR5 WG1 Chapter 8 Anthropogenic and \
		Natural Radiative Forcing. Table 8.SM.1 Supplementary for Table 8.3: RF \
		formulae for CO2, CH4 and N2O.
	|

global_surface_area=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'area')
	~	meter*meter
	~	Global surface area.
	|

Time_Const_for_PFC=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Time_Const_for_PFC'\
		)
	~	Years
	~	based on CF4
		From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

Time_Const_for_SF6=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Time_Const_for_SF6'\
		)
	~	Years
	~	From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

CH4_radiative_efficiency_coefficient=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_radiative_efficiency_coefficient'\
		)
	~	watt/(meter*meter)
	~	AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table \
		8.SM.1 Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O.
	|

CH4_reference_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'CH4_reference_conc'\
		)
	~	ppb
	~	WG1AR5_Chapter08_FINAL.pdf.  \
		https://www.ipcc.ch/pdf/assessment-report/ar5/wg1/WG1AR5_Chapter08_FINAL.pd\
		f
		722 ± 25 ppb
	|

Init_C_in_Humus=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_C_in_Humus'\
		)
	~	GtC
	~	Inital carbon in humus.
	|

Init_PFC_in_Atm_con=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_PFC_in_Atm'\
		)
	~	ppt
	~	Historical data. NASA. GISS. https://data.giss.nasa.gov/modelforce/ghgases/
	|

N2O_radiative_efficiency_coefficient=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'N2O_radiative_efficiency_coefficient'\
		)
	~	watt/(meter*meter)
	~	AR5 WG1 Chapter 8 Anthropogenic and Natural Radiative Forcing. Table \
		8.SM.1 Supplementary for Table 8.3: RF formulae for CO2, CH4 and N2O.
	|

GWP_100_year[GHGs]=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'GWP_100*'\
		 )
	~	Dmnl
	~	Warming caused by any greenhouse gas in 100 years as a multiple of the \
		warming caused by the same mass of carbon dioxide (CO2). GWP is 1 for CO2.
	|

GWP_20_year[GHGs]=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'GWP_20*'\
		 )
	~	Dmnl
	~	Warming caused by any greenhouse gas in 20 years as a multiple of the \
		warming caused by the same mass of carbon dioxide (CO2). GWP is 1 for CO2.
	|

Heat_Diffusion_Covar=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Heat_Diffusion_Covar'\
		)
	~	Dmnl
	~	Fraction of heat transfer that depends on eddy diffusion.
	|

pH_constant_4=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'pH_constant_4'\
		 )
	~	pH/(ppm*ppm*ppm)
	~	Bernie, D., J. Lowe, T. Tyrrell, and O. Legge (2010), Influence of \
		mitigation policy on ocean acidification, Geophys. Res. Lett., 37, L15704, \
		doi:10.1029/2010GL043181.
	|

Inital_HFC_con[HFC_type]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Initial_HFC_con*'\
		)
	~	ppt
	~		|

HFC_type:
	HFC134a	,
	HFC23	,
	HFC32	,
	HFC125	,
	HFC143a	,
	HFC152a	,
	HFC227ea	,
	HFC245ca	,
	HFC4310mee
	~	
	~	Hydrofluorocarbons.
	|

Init_C_in_Deep_Ocean_per_meter[Layers]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_C_in_Deep_Ocean_per_meter*'\
		)
	~	GtC/meter
	~	Initial carbon concentration in deep ocean layers.
	|

SF6_radiative_efficiency=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'SF6_radiative_efficiency'\
		)
	~	watt/(ppb*meter*meter)
	~	From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

Mixed_Depth=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Mixed_Depth'\
		)
	~	meter
	~	Mixed ocean layer depth.
	|

PFC_radiative_efficiency=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'PFC_radiative_efficiency'\
		)
	~	watt/(ppb*meter*meter)
	~	Radiative efficiency of CF4.
		From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

pH_constant_1=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'pH_constant_1'\
		 )
	~	pH
	~	Bernie, D., J. Lowe, T. Tyrrell, and O. Legge (2010), Influence of \
		mitigation policy on ocean acidification, Geophys. Res. Lett., 37, L15704, \
		doi:10.1029/2010GL043181.
	|

pH_constant_2=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'pH_constant_2'\
		 )
	~	pH/ppm
	~	Bernie, D., J. Lowe, T. Tyrrell, and O. Legge (2010), Influence of \
		mitigation policy on ocean acidification, Geophys. Res. Lett., 37, L15704, \
		doi:10.1029/2010GL043181.
	|

pH_constant_3=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'pH_constant_3'\
		 )
	~	pH/(ppm*ppm)
	~	Bernie, D., J. Lowe, T. Tyrrell, and O. Legge (2010), Influence of \
		mitigation policy on ocean acidification, Geophys. Res. Lett., 37, L15704, \
		doi:10.1029/2010GL043181.
	|

Sensitivity_of_pCO2_DIC_to_Temperature_Mean=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Sensitivity_of_pCO2_DIC_to_Temperature_Mean'\
		)
	~	1/DegreesC
	~	Sensitivity of equilibrium concentration of dissolved inorganic carbon to \
		temperature.  Calibrated to be consistent with Friedlingstein et al., \
		2006.  Climate-Carbon Cycle Feedback Analysis: ResuMCS from the C4MIP \
		Model Intercomparison.  Journal of Climate. p3337-3353.  Default \
		Sensitivity of C Uptake to Temperature of 1 corresponds to mean value from \
		the 11 models tested.
	|

init_Atmos_UOcean_Temp=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'init_Atmos_UOcean_Temp'\
		)
	~	DegreesC
	~	Global Annual Temperature Anomaly (Land + Ocean) in 1990 from NASA GISS Surface \
		Temperature (GISTEMP): +0.43 ºC.
		5-year average: +0.36 ºC. Average 1880-1889 = -0,225. Preindustrial reference: W,36 \
		+ W,225 = W,585
		http://cdiac.ornl.gov/ftp/trends/temp/hansen/gl_land_ocean.txt
	|

Init_C_in_Biomass=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_C_in_Biomass'\
		)
	~	GtC
	~	Initial carbon in biomass.
	|

Preind_Ocean_C_per_meter=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Preind_Ocean_C_per_meter'\
		)
	~	GtC/meter
	~	Corresponds with 767.8 GtC in a 75m layer.
	|

Preindustrial_C=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'preindustrial_C'\
		)
	~	GtC
	~	Preindustrial C content of atmosphere.
	|

SWITCH_Sensitivity_of_C_Uptake_to_Temperature=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Switches', 'Sensitivity_of_C_Uptake_to_Temperature'\
		)
	~	Dmnl [0,2.5]
	~	Strength of the feedback effect of temperature on uptake of C by land and \
		oceans. W means no temperature-carbon uptake feedback and default of 1 \
		yields the average value found in Friedlingstein et al., 2006.  \
		Climate-Carbon Cycle Feedback Analysis: ResuMCS from the C4MIP Model \
		Intercomparison.  Journal of Climate. p3337-3353.
	|

Reference_Temperature=
	GET_DIRECT_CONSTANTS( '/model_parameters/climate/climate.xlsx' , 'World' , 'Reference_Temperature'\
		 )
	~	DegreesC [-2,2]
	~	From V&R (2009) supplement, table S1.
	|

Time_Const_for_HFC[HFC_type]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Time_Const_for_HFC*'\
		)
	~	Years
	~	From AR5 WG1 Chapter 8.  Table 8.A.1. Lifetimes, Radiative Efficiencies \
		and Metric Values
	|

GHGs:
	CO2,
	CH4,
	N2O,
	PFCs,
	SF6,
	HFC134a,
	HFC23,
	HFC32,
	HFC125,
	HFC143a,
	HFC152a,
	HFC227ea,
	HFC245ca,
	HFC4310mee
	~	
	~		|

Mixing_Time=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Mixing_Time'\
		)
	~	Year [0.25,10]
	~	Atmosphere - mixed ocean layer mixing time.
	|

Preindustrial_PFC_conc=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Preindustrial_PFC_conc'\
		)
	~	ppt
	~		|

Init_Deep_Ocean_Temp[Layers]=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_Deep_Ocean_Temp*'\
		)
	~	DegreesC
	~	C-ROADS simulation
	|

Stratospheric_CH4_path_share=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Stratospheric_CH4_path_share'\
		)
	~	Dmnl [0,1]
	~	Calculated from AR5 WG1 Chapter 6
	|

Time_to_Commit_RF=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Time_to_Commit_RF'\
		)
	~	Year [1900,2200]
	~	Time after which forcing is frozen for a test of committed warming.
	|

N2O_N_molar_mass=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'N2O_N_molar_mass'\
		)
	~	
	~		|

SWITCH_Sensitivity_of_Methane_Emissions_to_Temperature=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Switches', 'Sensitivity_of_Methane_Emissions_to_Temperature'\
		)
	~	Dmnl [0,2.5]
	~	Allows users to control the strength of the feedback effect of temperature \
		on release of C as CH4 from humus. Default of W means no temperature \
		feedback and 1 is mean feedback.
	|

Eddy_diff_mean=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Eddy_diff_mean'\
		)
	~	meter*meter/Year [2000,8000]
	~	Rate of vertical transport and mixing in the ocean due to eddy diffusion \
		motion.
	|

land_thickness=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'land_thickness'\
		)
	~	meter
	~	Effective land area heat capacity, expressed as equivalent water layer \
		thickness.
	|

Tropospheric_CH4_path_share=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Tropospheric_CH4_path_share'\
		)
	~	Dmnl [0,1]
	~	Calculated from AR5 WG1 Chapter 6
	|

SWITCH_Sensitivity_of_Methane_Emissions_to_Permafrost_and_Clathrate=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx', 'Switches', 'Sensitivity_of_Methane_Emissions_to_Permafrost_and_Clathrate'\
		)
	~	Dmnl [0,1]
	~	0 = no feedback
		1 = base feedback
	|

Init_NPP=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Init_NPP')
	~	GtC/Year
	~	Initial net primary production. Adapted from Goudriaan, 1984.
	|

Time_Const_for_N2O=
	GET_DIRECT_CONSTANTS('/model_parameters/climate/climate.xlsx', 'World', 'Time_Const_for_N2O'\
		)
	~	Years
	~	Value of CH4 and N2O time constants reported in AR5 WG1 Chapter 8 Table \
		8.A.1 noted to be for calculation of GWP, not for cycle. Value of 117 \
		years determined through optimization.
	|

Desired_government_consumption=
	SUM(Desired_government_consumption_by_sector[SECTORS!])
	~	
	~		|

INDUSTRIAL_ROUNDWOOD_INTENSITY[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'INDUSTRIAL_ROUNDWOOD_INTENSITY'\
		)
	~	
	~		|

Forrmal_economy_to_subsistence[REGION,AGE_COHORTS]=
	SUM(Population_in_formal_economy[REGION,AGE_COHORTS]*SHARE_OF_POPULATION_PER_CLASS[CLASS\
		!]*rate_of_people_that_want_to_incorporate_to_subsistence[REGION,CLASS!])*MIN(1,ZIDZ\
		(Maximum_population_in_subsistence-SUM(Population_in_subsistence[REGION!,AGE_COHORTS\
		!]),SUM(Population_in_formal_economy[REGION!,AGE_COHORTS!]*SHARE_OF_POPULATION_PER_CLASS\
		[CLASS!]*rate_of_people_that_want_to_incorporate_to_subsistence[REGION!,CLASS!])))
	~	
	~		|

Water_use=
	SUM(Water_use_by_type[WATER!])
	~	
	~		|

Material_extracción_unused[MATERIALS]=
	(SUM(MATERIAL_EXTRACTION_INTENSITY_UNUSED[MATERIALS,SECTORS!]*Output_by_sector[SECTORS\
		!]))/10^3
	~	Mt
	~	original value in kt -> conver to Mt
	|

Material_extraction_for_renewables[MATERIALS]=
	Material_extraction_used[MATERIALS,lot_re_wind]+Material_extraction_used[MATERIALS,lot_re_PV\
		]+Material_extraction_used[MATERIALS,lot_re_stherm]
	~	Mt
	~		|

AIR_POLLUTION_S:
	NH3,
	PM2_5,
	PM10
	~	
	~		|

INITIAL_AIR_POLLUTION_SECTORIAL_INTENSITY[AIR_POLLUTION_S,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'AIR_POLLUTION_SECTORIAL_INTENSITY'\
		)
	~	
	~		|

WATER:
	green, blue
	~	
	~		|

INITIAL_WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'WATER_CONSUMPTION_INTENSITY_OF_HOUSEHOLDS'\
		)
	~	
	~		|

EMISSIONS:
	CO2,
	CH4,
	N2O,
	SF6,
	HFC134a,
	PFCs
	~	
	~		|

MATERIALS:
	Bauxite_and_aluminium,
	Copper,
	Gold,
	Iron,
	Lead,
	Nickel,
	Other_non_ferrous_metal,
	PGM,
	Silver,
	Tin,
	Zinc,
	Building_stones,
	Chemical_and_fertilizer_minerals,
	Clays_and_kaolin,
	Gravel_and_sand,
	Limestone_gypsum_chalk_dolomite,
	Other_minerals,
	Salt,
	Slate
	~	
	~		|

INITIAL_NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE[NITROGEN_PHOSPHORUS_POLLUTION\
		,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'NITROGEN_AND_PHOSPHORUS_POLLUTION_INTENSITY_OF_AGRICULTURE'\
		)
	~	
	~		|

NITROGEN_PHOSPHORUS_POLLUTION:
	Nitrogen_water,
	Phosphorus_soil,
	Phosphorus_water
	~	
	~		|

MATERIAL_EXTRACTION_INTENSITY_USED[MATERIALS,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'MATERIAL_EXTRACTION_INTENSITY_USED'\
		)
	~	
	~		|

LAND_EMISSIONS:
	infrastructure,
	energy_land,
	food_land_capitalism,
	food_land_subsistence,
	other_land
	~	
	~		|

LAND_USE_CHANGE_EMISSIONS_INTENSITY[LAND_EMISSIONS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'LAND_USE_CHANGE_EMISSIONS_INTENSITY*'\
		)
	~	
	~		|

Land_variation[LAND]=
	Land_distribution[LAND]-Delayed_land_distribution[LAND]
	~	
	~		|

Delayed_land_distribution[LAND]=
	delay_fixed(Land_distribution[LAND],1,Land_distribution[LAND])
	~	
	~		|

INITIAL_WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'WATER_WITHDRAWAL_INDUSTRIAL_INTENSITY'\
		)
	~	
	~		|

Population_in_subsistence[REGION,C_0_4]= INTEG (
	Births_subsistence[REGION]+Forrmal_economy_to_subsistence[REGION,C_0_4]-Subsistence_to_formal_economy\
		[REGION,C_0_4]-Deaths_subsistence
	[REGION,C_0_4]-Population_in_subsistence[REGION,C_0_4]/5,
		INITIAL_POPULATION_IN_SUBSISTENCE[REGION,C_0_4]) ~~|
Population_in_subsistence[REGION,age_middle]= INTEG (
	Population_in_subsistence[REGION,age_young]/5+Forrmal_economy_to_subsistence[REGION,\
		age_middle]-Subsistence_to_formal_economy
	[REGION,age_middle]-Deaths_subsistence[REGION,age_middle]-Population_in_subsistence[\
		REGION,age_middle]/5,
		INITIAL_POPULATION_IN_SUBSISTENCE[REGION,age_middle]) ~~|
Population_in_subsistence[REGION,C_95_plus]= INTEG (
	Population_in_subsistence[REGION,C_90_94]/5+Forrmal_economy_to_subsistence[REGION,C_95_plus\
		]-Subsistence_to_formal_economy
	[REGION,C_95_plus]-Deaths_subsistence[REGION,C_95_plus],
		INITIAL_POPULATION_IN_SUBSISTENCE[REGION,C_95_plus])
	~	person
	~		|

MATERIAL_EXTRACTION_INTENSITY_UNUSED[MATERIALS,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'MATERIAL_EXTRACTION_INTENSITY_UNUSED'\
		)
	~	
	~		|

INITIAL_GREENHOUSE_GAS_EMISSIONS_INTENSITY[EMISSIONS,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'GREENHOUSE_GAS_EMISSIONS_INTENSITY'\
		)
	~	
	~		|

INITIAL_WATER_CONSUMPTION_INDUSTRIAL_INTENSITY[WATER,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'WATER_INDUSTRIAL_INTENSITY'\
		)
	~	
	~		|

Industrial_roundwood=
	SUM(Output_by_sector[SECTORS!]*INDUSTRIAL_ROUNDWOOD_INTENSITY[SECTORS!])
	~	
	~		|

INITIAL_WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Stressors' , 'WATER_WITHDRAWAL_INTENSITY_OF_HOUSEHOLD'\
		)
	~	
	~		|

Total_material_extraction[MATERIALS]=
	Material_extraction_used[MATERIALS,erebor]
	~	Mt
	~	everything before already converted in Mt
	|

Births_subsistence[REGION]=
	SUM(Births_per_age_cohort_subsistence[REGION,AGE_COHORTS!])
	~	person/Year
	~		|

Deaths_subsistence[REGION,AGE_COHORTS]=
	Population_in_subsistence[REGION,AGE_COHORTS]*Mortality_rate_subsistence[REGION,AGE_COHORTS\
		]
	~	person/Year
	~		|

Births_per_age_cohort_subsistence[REGION,AGE_COHORTS]=
	Population_in_subsistence[REGION,AGE_COHORTS]*Birth_rate_subsistence[REGION,AGE_COHORTS\
		]
	~	person/Year
	~		|

Mortality_rate_subsistence[REGION,AGE_COHORTS]=
	Mortality_rate_over_five_years_subsistence[REGION,AGE_COHORTS]/5
	~	1/Year
	~		|

Birth_rate_subsistence[REGION,AGE_COHORTS]=
	Birth_rate_over_five_years_subsistence[REGION,AGE_COHORTS]/5
	~	1/Year
	~		|

Population_in_formal_economy[REGION,C_0_4]= INTEG (
	Births_formal_economy[REGION]-Deaths_formal_econoy[REGION,C_0_4]+Subsistence_to_formal_economy\
		[REGION,C_0_4]-Forrmal_economy_to_subsistence[REGION,C_0_4]-Population_in_formal_economy\
		[REGION,C_0_4]/5,
		INITIAL_POPULATION_IN_FORMAL_ECONOMY[REGION,C_0_4]) ~~|
Population_in_formal_economy[REGION,age_middle]= INTEG (
	Population_in_formal_economy[REGION,age_young]/5-Deaths_formal_econoy[REGION,age_middle\
		]+Subsistence_to_formal_economy[REGION,age_middle]-Forrmal_economy_to_subsistence[REGION\
		,age_middle]-Population_in_formal_economy[REGION,age_middle]/5,
		INITIAL_POPULATION_IN_FORMAL_ECONOMY[REGION,age_middle]) ~~|
Population_in_formal_economy[REGION,C_95_plus]= INTEG (
	Population_in_formal_economy[REGION,C_90_94]/5+Subsistence_to_formal_economy[REGION,\
		C_95_plus]-Forrmal_economy_to_subsistence[REGION,C_95_plus]-Deaths_formal_econoy[REGION\
		,C_95_plus],
		INITIAL_POPULATION_IN_FORMAL_ECONOMY[REGION,C_95_plus])
	~	person
	~		|

Birth_rate_over_five_years_subsistence[REGION,C_15_19]=
	MAX(0,YF_BIRTH_RATE[C_15_19]+ (Y0_BIRTH_RATE[C_15_19] - YF_BIRTH_RATE[C_15_19] )* EXP
	(-EXP(LOG_ALPHA_BIRTH_RATE[C_15_19]) * CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION]\
		)) ~~|
Birth_rate_over_five_years_subsistence[REGION,C_25_29]=
	MAX(0,YF_BIRTH_RATE[C_25_29] + (Y0_BIRTH_RATE[C_25_29] - YF_BIRTH_RATE[C_25_29]) * EXP\
		(-ALPHA_BIRTH_RATE[C_25_29]*CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION])) ~~|
Birth_rate_over_five_years_subsistence[REGION,C_30_34]=
	MAX(0,BETA_1_BIRTH_RATE[C_30_34]+BETA_2_BIRTH_RATE[C_30_34]*LN(CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION])) ~~|
Birth_rate_over_five_years_subsistence[REGION,C_35_39]=
	MAX(0,MIN(0.25,BETA_1_BIRTH_RATE[C_35_39] + BETA_2_BIRTH_RATE[C_35_39]*CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION])) ~~|
Birth_rate_over_five_years_subsistence[REGION,C_20_24]=
	MAX(0,YF_BIRTH_RATE[C_20_24]+ (Y0_BIRTH_RATE[C_20_24] - YF_BIRTH_RATE[C_20_24] )* EXP
	(-EXP(LOG_ALPHA_BIRTH_RATE[C_20_24]) * CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION]\
		)) ~~|
Birth_rate_over_five_years_subsistence[REGION,C_40_44]=
	MAX(0,YF_BIRTH_RATE[C_40_44] + (Y0_BIRTH_RATE[C_40_44] - YF_BIRTH_RATE[C_40_44]) * EXP\
		(-ALPHA_BIRTH_RATE[C_40_44]
	 * CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION])) ~~|
Birth_rate_over_five_years_subsistence[REGION,UNFERTILE_AGE]=
	0
	~	1/Year
	~	YF_BIRTH_RATE[C_15_19]+ (Y0_BIRTH_RATE[C_15_19] - YF_BIRTH_RATE[C_15_19] )* EXP
		(-EXP(LOG_ALPHA_BIRTH_RATE[C_15_19]) * \
		(Consumption_per_capita[REGION,CLASS]+Government_education_expenditure_per_\
		capita[REGION]))
		BETA_1_BIRTH_RATE[C 30 34]+BETA_2_BIRTH_RATE[C 30 \
		34]*LN(Consumption_per_capita[REGION,CLASS!]+Government_education_expenditu\
		re_per_capita[REGION])
	|

PTYPE_LAND_SP[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'PTYPE_LAND_MP'\
		)
	~	
	~		|

Infraestructure_demand=
	Desired_consumption*INFRAESTRUCTURE_LAND_INTENSITY
	~	
	~		|

INFRAESTRUCTURE_LAND_INTENSITY=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'INFRAESTRUCTURE_LAND_INTENSITY'\
		)
	~	
	~		|

Desired_consumption=
	SUM(Desired_consumption_by_sector[SECTORS!])
	~	
	~		|

UNUSED_FOREST:
	primary_forest,
	secondary_forest
	~	
	~		|

PPRIORITY_LAND_SP[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'PPRIORITY_LAND_MP'\
		)
	~	
	~		|

INITIAL_UNUSED_FOREST[UNUSED_FOREST]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'INITIAL_FOREST_LAND*'\
		)
	~	
	~		|

REST_OF_THE_LANDS:
	infrastructure,
	energy_land,
	other_land,
	shrub
	~	
	~		|

PEXTRA_LAND_SP[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'PEXTRA_LAND_MP'\
		)
	~	
	~		|

INITIAL_SECTORIAL_LANDS_INTENSITIES[SECTORIAL_LANDS,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'INITIAL_SECTORIAL_LANDS_INTENSITIES'\
		)
	~	
	~		|

Sectorial_land_intensities_before_damage[SECTORIAL_LANDS,SECTORS]=
	if_then_else(TARGET_LAND_INTENSITIES_SP[SECTORIAL_LANDS,SECTORS]=0,INITIAL_SECTORIAL_LANDS_INTENSITIES\
		[SECTORIAL_LANDS,SECTORS]+RAMP(ZIDZ(TARGET_LAND_INTENSITIES_SP[SECTORIAL_LANDS,SECTORS\
		]-INITIAL_SECTORIAL_LANDS_INTENSITIES[SECTORIAL_LANDS,SECTORS],2100-INITIAL_TIME), \
		INITIAL_TIME , 2100),INITIAL_SECTORIAL_LANDS_INTENSITIES[SECTORIAL_LANDS,SECTORS]*(\
		1+Land_intensity_growth_rate[SECTORIAL_LANDS,SECTORS])^(Time-INITIAL_TIME))
	~	
	~		|

SECTORIAL_LANDS:
	energy_land,
	food_land_capitalism,
	forest_land,
	other_land
	~	
	~		|

TARGET_LAND_INTENSITIES_SP[SECTORIAL_LANDS,SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'TARGET_LAND_INTENSITIES_SP'\
		)
	~	
	~		|

LAND:
	infrastructure,
	energy_land,
	food_land_capitalism,
	food_land_subsistence,
	forest_land,
	primary_forest,
	secondary_forest,
	other_land,
	shrub
	~	
	~		|

Land_demand_for_human_use[infrastructure]=
	Infraestructure_demand ~~|
Land_demand_for_human_use[energy_land]=
	Sectorial_land_demand[energy_land] ~~|
Land_demand_for_human_use[food_land_capitalism]=
	Sectorial_land_demand[food_land_capitalism] ~~|
Land_demand_for_human_use[food_land_subsistence]=
	Foodland_demand_for_subsistence ~~|
Land_demand_for_human_use[forest_land]=
	Sectorial_land_demand[forest_land] ~~|
Land_demand_for_human_use[other_land]=
	Sectorial_land_demand[other_land]
	~	
	~		|

Land_intensity_growth_rate[SECTORIAL_LANDS,SECTORS]=
	ZIDZ(TARGET_LAND_INTENSITIES_SP[SECTORIAL_LANDS,SECTORS],INITIAL_SECTORIAL_LANDS_INTENSITIES\
		[SECTORIAL_LANDS,SECTORS])^(1/(2100-INITIAL_TIME))-1
	~	
	~		|

FOODLAND_AND_FOREST:
	food_land_capitalism,
	food_land_subsistence,
	primary_forest,
	secondary_forest,
	shrub
	~	
	~		|

PWIDTH_LAND_SP[LAND]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Land' , 'PWIDTH_LAND_MP'\
		)
	~	
	~		|

Land_distribution[LAND]=
	ALLOCATE_AVAILABLE(Land_demand[LAND],Foodland_and_forest_priority_vector[LAND,ptype]\
		,Disposable_land)
	~	
	~	ALLOCATE_AVAILABLE(Land_demand[LAND],Foodland_and_forest_priority_vector[LA\
		ND,ptype],Disposable_land)
	|

INITIAL_SUBSISTENCE_LAND_INTENSITY=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Land' , 'SUBSISTENCE_LAND_INTENSITY'\
		)
	~	
	~		|

Desired_final_demand=
	SUM(Desired_final_demand_by_sector[SECTORS!])
	~	
	~		|

BETA_1_SUBSISTENCE_TO_FORMAL_ECONOMY_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Population' ,\
		 'BETA_1_SUBSISTENCE_TO_FORMAL_ECONOMY')
	~	
	~		|

BETA_0_FORMAL_ECONOMY_TO_SUBSISTENCE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Population' ,\
		 'BETA_0_FORMAL_ECONOMY_TO_SUBSISTENCE')
	~	
	~		|

BETA_1_FORMAL_ECONOMY_TO_SUBSISTENCE_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Population' ,\
		 'BETA_1_FORMAL_ECONOMY_TO_SUBSISTENCE')
	~	
	~		|

Mortality_scarcity_factor=
	if_then_else(prod(Delayed_time_step_mortality_rate[REGION!,AGE_COHORTS!])=1,0,1)
	~	
	~		|

Labour_intensity_before_damage[SECTORS]=
	if_then_else(TARGET_LABOUR_INTENSITY_SP[SECTORS]=0,INITIAL_LABOUR_INTENSITY[SECTORS]\
		+RAMP(ZIDZ(TARGET_LABOUR_INTENSITY_SP[SECTORS
	]-INITIAL_LABOUR_INTENSITY[SECTORS],2100-INITIAL_TIME), INITIAL_TIME , 2100),INITIAL_LABOUR_INTENSITY\
		[SECTORS]*(1+Labour_intensity_growth_rate[SECTORS])^(Time-INITIAL_TIME))
	~	
	~		|

Delayed_time_step_mortality_rate[REGION,AGE_COHORTS]= delay_fixed (
	Mortality_rate_formal_economy[REGION,AGE_COHORTS],TIME_STEP,0)
	~	
	~		|

TARGET_LABOUR_INTENSITY_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Labour' , 'TARGET_LABOUR_INTENSITY'\
		)
	~	
	~		|

Labour_intensity_growth_rate[SECTORS]=
	ZIDZ(TARGET_LABOUR_INTENSITY_SP[SECTORS],INITIAL_LABOUR_INTENSITY[SECTORS])^(1/(2100\
		-INITIAL_TIME))-1
	~	
	~		|

Target_growth_rate_A_matrix[SECTORS,SECTORS1]=
	ZIDZ(A_MATRIX_2100[SECTORS,SECTORS1],INITIAL_A_MATRIX[SECTORS,SECTORS1])^(1/(2100-INITIAL_TIME\
		))-1
	~	
	~		|

ANNUAL_WORKING_HOURS_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Labour' , 'ANNUAL_WORKING_HOURS'\
		)
	~	hours_per_person
	~		|

Total_labour_demand=
	SUM(Labour_demand[SECTORS!])
	~	
	~		|

INITIAL_LABOUR_INTENSITY[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Labour' , 'INITIAL_LABOUR_INTENSITY'\
		)
	~	
	~		|

Workforce_utilization_rate=
	ZIDZ(Total_labour_demand,Maximum_labour_supply)
	~	
	~		|

WORKING_AGE_POPULATION:
	C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44, C_45_49, C_50_54, C_55_59, C_60_64
	~	
	~		|

Recoverable_resources_of_fossil_fuels= INTEG (
	-Fossil_fuel_depletion,
		INITIAL_RECOVERABLE_RESOURCES_OF_FOSSIL_FUELS_SP)
	~	
	~		|

FOSSIL_FUELS:
	oil, natural_gas, coal
	~	
	~		|

CONVERSION_FACTOR_MONETARY_TO_ENERGY[ENERGY,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Energy' , 'CONVERSION_FACTOR_MONETARY_TO_ENERGY'\
		)
	~	
	~		|

Desired_final_energy_resources_used_by_type[ENERGY]=
	SUM(Desired_final_energy_by_sector_and_type[ENERGY,SECTORS!])+Desired_non_energy_use_of_fossil_fuels\
		[ENERGY]
	~	
	~		|

BETA_0_EXTRACTION_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Energy' , 'BETA_0_EXTRACTION'\
		)
	~	
	~		|

ENERGY:
	oil, natural_gas, coal, electricity, biofuels_waste, other_final_energy
	~	
	~		|

Total_output=
	SUM(Output_by_sector[SECTORS!])
	~	
	~		|

BETA_1_EXTRACTION_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Energy' , 'BETA_1_EXTRACTION'\
		)
	~	
	~		|

CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_URANIUM=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Energy' , 'CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_URANIUM'\
		)
	~	
	~		|

CONVERSION_FACTOR_MONETARY_TO_NON_ENERGY_USE_OF_FOSSIL_FUELS[ENERGY,SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Energy' , 'CONVERSION_FACTOR_MONETARY_TO_NON_ENERGY_USE_OF_FOSSIL_FUELS'\
		)
	~	
	~		|

CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_FOSSIL_FUELS[FOSSIL_FUELS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Energy' , 'CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_FOSSIL_FUELS*'\
		)
	~	
	~		|

Desired_primary_energy_of_uranium=
	Desired_final_energy_by_sector_and_type[electricity,lot_nuc]*CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_URANIUM
	~	
	~		|

INITIAL_RECOVERABLE_RESOURCES_OF_FOSSIL_FUELS_SP=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Energy' , 'INITIAL_RECOVERABLE_RESOURCES_OF_FOSSIL_FUELS'\
		)
	~	
	~		|

Desired_primary_energy_of_fossil_fuels_by_type[FOSSIL_FUELS]=
	Desired_final_energy_resources_used_by_type[FOSSIL_FUELS]*CONVERSION_FROM_FINAL_ENERGY_TO_PRIMARY_ENERGY_FOSSIL_FUELS\
		[FOSSIL_FUELS]
	~	
	~		|

Desired_consumption_by_region_and_class[REGION,CLASS]=
	Desired_consumption_per_capita[REGION,CLASS]*Population_by_region_and_class[REGION,CLASS\
		]*MATRIX_UNITS_PREFIXES[BASE_UNIT,mega]
	~	million_euro/Year
	~		|

Government_education_expenditure_per_capita[REGION]=
	MAX(1,Government_consumption_by_sector_and_region[REGION,riv_educ]*MATRIX_UNITS_PREFIXES\
		[mega,BASE_UNIT]/Total_population_in_formal_economy_by_region[REGION])
	~	euro/person
	~		|

Government_health_expenditure_per_capita[REGION]=
	MAX(1,ZIDZ(Government_consumption_by_sector_and_region[REGION,riv_health]*MATRIX_UNITS_PREFIXES\
		[mega,BASE_UNIT],Total_population_in_formal_economy_by_region[REGION]))
	~	euro/person
	~		|

Consumption_per_capita[Centre,high]=
	ZIDZ(Final_demand_by_components[consumption_center_high],Population_by_region_and_class\
		[Centre,high])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Centre,medium]=
	ZIDZ(Final_demand_by_components[consumption_center_medium],Population_by_region_and_class\
		[Centre,medium])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Centre,low]=
	ZIDZ(Final_demand_by_components[consumption_center_low],Population_by_region_and_class\
		[Centre,low])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Semiperiphery,high]=
	ZIDZ(Final_demand_by_components[consumption_semiperiphery_high],Population_by_region_and_class\
		[Semiperiphery,high])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Semiperiphery,medium]=
	ZIDZ(Final_demand_by_components[consumption_semiperiphery_medium],Population_by_region_and_class\
		[Semiperiphery,medium])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Semiperiphery,low]=
	ZIDZ(Final_demand_by_components[consumption_semiperiphery_low],Population_by_region_and_class\
		[Semiperiphery,low])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Periphery,high]=
	ZIDZ(Final_demand_by_components[consumption_periphery_high],Population_by_region_and_class\
		[Periphery,high])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Periphery,medium]=
	ZIDZ(Final_demand_by_components[consumtion_periphery_medium],Population_by_region_and_class\
		[Periphery,medium])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT] ~~|
Consumption_per_capita[Periphery,low]=
	ZIDZ(Final_demand_by_components[consumption_periphery_low],Population_by_region_and_class\
		[Periphery,low])*MATRIX_UNITS_PREFIXES[mega,BASE_UNIT]
	~	euro/(person*Year)
	~		|

Desired_consumption_per_capita_by_region[REGION]=
	SUM(Desired_consumption_per_capita[REGION,CLASS!]*SHARE_OF_POPULATION_PER_CLASS[CLASS\
		!])
	~	euro/(person*Year)
	~		|

Desired_consumption_per_capita_not_covered[REGION,CLASS]=
	Desired_consumption_per_capita[REGION,CLASS]-Consumption_per_capita[REGION,CLASS]
	~	euro/(person*Year*Year)
	~	Desired_consumption_per_capita[REGION,CLASS]-Consumption_per_capita[REGION,\
		CLASS]
	|

MATRIX_UNITS_PREFIXES[unit_prefixes,unit_prefixes_1]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Units' , 'MATRIX_UNITS_PREFIXES'\
		)
	~	
	~		|

unit_prefixes_1:
	pico,nano,micro,mili,centi,deci,BASE_UNIT,deca,hecto,kilo,mega,giga,tera,peta,exa,zetta
	~	
	~		|

unit_prefixes:
	pico,nano,micro,mili,centi,deci,BASE_UNIT,deca,hecto,kilo,mega,giga,tera,peta,exa,zetta
	~	
	~		|

Desired_consumption_by_region[REGION]=
	SUM(Population_by_region_and_class[REGION,CLASS!])*Desired_consumption_per_capita_by_region
	[REGION]*MATRIX_UNITS_PREFIXES[BASE_UNIT,mega]
	~	million_euro/Year
	~		|

GOVERNMENT_DEMAND:
	government_center, government_semiperiphery, government_periphery -> REGION
	~	
	~		|

Final_demand_by_components[DEMAND_COMPONENTS]=
	ALLOCATE_AVAILABLE(Desired_final_demand_by_components[DEMAND_COMPONENTS],Demand_priority_vector\
		[DEMAND_COMPONENTS,ptype],Final_demand)
	~	million_euro/Year
	~		|

pprofile:
	ptype, ppriority, pwidth, pextra
	~	
	~		|

PTYPE_DEMAND_MP[DEMAND_COMPONENTS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'PTYPE_DEMAND_MP'\
		)
	~	1
	~		|

Capital_stock[SECTORS]= INTEG (
	Investment_by_sector[SECTORS]-Depreciation_by_sector[SECTORS],
		Initial_capital_stock[SECTORS])
	~	
	~		|

PWIDTH_DEMAND_MP[DEMAND_COMPONENTS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'PWIDTH_DEMAND_MP'\
		)
	~	1
	~		|

CONSUMPTION_DEMAND:
	consumption_center_high, consumption_center_medium, consumption_center_low, consumption_semiperiphery_high\
		, consumption_semiperiphery_medium, consumption_semiperiphery_low, consumption_periphery_high\
		, consumtion_periphery_medium, consumption_periphery_low
	~	
	~		|

Investment_by_sector[SECTORS]=
	Desired_investment_by_sector[SECTORS]*Scarcitiy_factor_for_investment
	~	
	~		|

PEXTRA_DEMAND_MP[DEMAND_COMPONENTS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'PEXTRA_DEMAND_MP'\
		)
	~	1
	~		|

PPRIORITY_DEMAND_MP[DEMAND_COMPONENTS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'PPRIORITY_DEMAND_MP'\
		)
	~	1
	~		|

Desired_final_demand_by_components[Investment]=
	Desired_gross_fixed_capital_formation ~~|
Desired_final_demand_by_components[GOVERNMENT_DEMAND]=
	Desired_government_consumption_by_region[REGION] ~~|
Desired_final_demand_by_components[consumption_center_high]=
	Desired_consumption_by_region_and_class[Centre,high] ~~|
Desired_final_demand_by_components[consumption_center_medium]=
	Desired_consumption_by_region_and_class[Centre,medium] ~~|
Desired_final_demand_by_components[consumption_center_low]=
	Desired_consumption_by_region_and_class[Centre,low] ~~|
Desired_final_demand_by_components[consumption_semiperiphery_high]=
	Desired_consumption_by_region_and_class[Semiperiphery,high] ~~|
Desired_final_demand_by_components[consumption_semiperiphery_medium]=
	Desired_consumption_by_region_and_class[Semiperiphery,medium] ~~|
Desired_final_demand_by_components[consumption_semiperiphery_low]=
	Desired_consumption_by_region_and_class[Semiperiphery,low] ~~|
Desired_final_demand_by_components[consumption_periphery_high]=
	Desired_consumption_by_region_and_class[Periphery,high] ~~|
Desired_final_demand_by_components[consumtion_periphery_medium]=
	Desired_consumption_by_region_and_class[Periphery,medium] ~~|
Desired_final_demand_by_components[consumption_periphery_low]=
	Desired_consumption_by_region_and_class[Periphery,low]
	~	million_euro/Year
	~		|

DEMAND_COMPONENTS:
	Investment, government_center, government_semiperiphery, government_periphery, consumption_center_high\
		, consumption_center_medium, consumption_center_low, consumption_semiperiphery_high\
		, consumption_semiperiphery_medium, consumption_semiperiphery_low, consumption_periphery_high\
		, consumtion_periphery_medium, consumption_periphery_low
	~	
	~		|

Demand_priority_vector[DEMAND_COMPONENTS, ptype]=
	PTYPE_DEMAND_MP[DEMAND_COMPONENTS] ~~|
Demand_priority_vector[DEMAND_COMPONENTS, ppriority]=
	PPRIORITY_DEMAND_MP[DEMAND_COMPONENTS] ~~|
Demand_priority_vector[DEMAND_COMPONENTS, pwidth]=
	PWIDTH_DEMAND_MP[DEMAND_COMPONENTS] ~~|
Demand_priority_vector[DEMAND_COMPONENTS, pextra]=
	PEXTRA_DEMAND_MP[DEMAND_COMPONENTS]
	~	1
	~		|

Desired_gross_fixed_capital_formation=
	SUM(Desired_gross_fixed_capital_formation_by_sector[SECTORS!])
	~	million_euro/Year
	~		|

Scarcitiy_factor_for_investment=
	ZIDZ(Final_demand_by_components[Investment],Desired_gross_fixed_capital_formation)
	~	1
	~		|

Final_demand_by_sector[SECTORS]=
	Desired_final_demand_by_sector[SECTORS]*Scarcity_factor
	~	
	~		|

Final_demand=
	SUM(Final_demand_by_sector[SECTORS!])
	~	
	~		|

BETA_1_MORTALITY_RATE_UNDER_SUBSISTENCE[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_1_MORTALITY_RATE'\
		)
	~	
	~		|

Birth_rate_over_five_years_formal_economy[REGION,C_15_19]=
	MAX(0,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE
	[C_15_19]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE[C_15_19]*Consumption_per_capita[REGION\
		,CLASS!],YF_BIRTH_RATE[C_15_19]+ (Y0_BIRTH_RATE
	[C_15_19] - YF_BIRTH_RATE[C_15_19] )* EXP
	(-EXP(LOG_ALPHA_BIRTH_RATE[C_15_19]) * (Consumption_per_capita[REGION,CLASS!]+Government_education_expenditure_per_capita
	[REGION])))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,C_25_29]=
	MAX(0,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE
	[C_25_29]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE[C_25_29]*Consumption_per_capita[REGION\
		,CLASS!],YF_BIRTH_RATE[C_25_29] + (Y0_BIRTH_RATE[C_25_29] - YF_BIRTH_RATE[C_25_29])\
		 * EXP(-ALPHA_BIRTH_RATE[C_25_29]
	 * (Consumption_per_capita[REGION,CLASS!]+Government_education_expenditure_per_capita\
		[REGION])))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,C_30_34]=
	MAX(0,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE
	[C_30_34]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE[C_30_34]*Consumption_per_capita[REGION\
		,CLASS!],BETA_1_BIRTH_RATE[C_30_34]+BETA_2_BIRTH_RATE[C_30_34]*LN(Consumption_per_capita\
		[REGION,CLASS!]+Government_education_expenditure_per_capita[REGION]))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,C_35_39]=
	MAX(0,SUM(MIN(0.25,if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE
	[C_35_39]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE[C_35_39]*Consumption_per_capita[REGION\
		,CLASS!],BETA_1_BIRTH_RATE[C_35_39] + BETA_2_BIRTH_RATE[C_35_39]*(Consumption_per_capita\
		[REGION,CLASS!]+Government_education_expenditure_per_capita
	[REGION])))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,C_20_24]=
	MAX(0,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE[C_20_24]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE\
		[C_20_24]*Consumption_per_capita[REGION,CLASS!],YF_BIRTH_RATE[C_20_24]+ (Y0_BIRTH_RATE\
		[C_20_24] - YF_BIRTH_RATE[C_20_24] )* EXP
	(-EXP(LOG_ALPHA_BIRTH_RATE[C_20_24]) * (Consumption_per_capita[REGION,CLASS!]+Government_education_expenditure_per_capita
	[REGION])))*SHARE_OF_POPULATION_PER_CLASS[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,C_40_44]=
	MAX(0,SUM(if_then_else(Consumption_per_capita[REGION,CLASS!]<CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE\
		[REGION],BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE[C_40_44]+BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE\
		[C_40_44]*Consumption_per_capita[REGION,CLASS!],YF_BIRTH_RATE[C_40_44] + (Y0_BIRTH_RATE\
		[C_40_44] - YF_BIRTH_RATE[C_40_44]) * EXP(-ALPHA_BIRTH_RATE[C_40_44]
	 * (Consumption_per_capita[REGION,CLASS!]+Government_education_expenditure_per_capita\
		[REGION])))*SHARE_OF_POPULATION_PER_CLASS
	[CLASS!])) ~~|
Birth_rate_over_five_years_formal_economy[REGION,UNFERTILE_AGE]=
	0
	~	1/Year
	~	YF_BIRTH_RATE[C_15_19]+ (Y0_BIRTH_RATE[C_15_19] - YF_BIRTH_RATE[C_15_19] )* EXP
		(-EXP(LOG_ALPHA_BIRTH_RATE[C_15_19]) * \
		(Consumption_per_capita[REGION,CLASS]+Government_education_expenditure_per_\
		capita[REGION]))
		BETA_1_BIRTH_RATE[C 30 34]+BETA_2_BIRTH_RATE[C 30 \
		34]*LN(Consumption_per_capita[REGION,CLASS!]+Government_education_expenditu\
		re_per_capita[REGION])
	|

BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE[FERTILE_AGE]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_0_BIRTH_RATE_UNDER_SUBSISTENCE'\
		)
	~	
	~		|

BETA_0_MORTALITY_RATE_UNDER_SUBSISTENCE[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_0_MORTALITY_RATE'\
		)
	~	
	~		|

BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE[FERTILE_AGE]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_1_BIRTH_RATE_UNDER_SUBSISTENCE'\
		)
	~	
	~		|

INITIAL_POPULATION_IN_SUBSISTENCE[REGION,AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'INITIAL_POPULATION_IN_SUBSISTENCE'\
		)
	~	
	~		|

GOVERNMENT_CONSUMPTION_AS_SHARE_OF_HOUSEHOLDS_CONSUMPTION_BY_REGION[REGION]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'GOVERNMENT_CONSUMPTION_AS_SHARE_OF_HOUSEHOLDS_CONSUMPTION_PER_EACH_CONSUMPTION_PER_CAPITA'\
		)
	~	(person*Year)/euro
	~		|

CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE[REGION]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_PER_CAPITA_IN_SUBSISTENCE*'\
		)
	~	euro/(person*Year)
	~		|

Desired_government_consumption_by_sector[SECTORS]=
	SUM(Desired_government_consumption_by_sector_and_region[REGION!,SECTORS])
	~	million_euro/Year
	~		|

Desired_output_by_sector[SECTORS1]=
	SUM(Leontief_matrix[SECTORS1,SECTORS!]*Desired_final_demand_by_sector[SECTORS!])
	~	million_euro/Year
	~		|

INITIAL_CAPITAL_INTENSITY[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_CAPITAL_INTENSITY'\
		)
	~	
	~		|

CAPITAL_INTENSITY_2100_SP[SECTORS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'CAPITAL_INTENSITY_2100'\
		)
	~	
	~	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , \
		'Economy' , 'CAPITAL_INTENSITY_2100')
	|

Delayed_time_step_output_by_sector[SECTORS]=
	delay_fixed(Output_by_sector[SECTORS],TIME_STEP, INITIAL_OUTPUT[SECTORS])
	~	million_euro/Year
	~		|

Output_by_sector[SECTORS]=
	Desired_output_by_sector[SECTORS]*Scarcity_factor
	~	million_euro/Year
	~		|

INITIAL_OUTPUT[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_OUTPUT'\
		)
	~	
	~		|

Desired_consumption_by_region_class_and_sector[REGION,CLASS,SECTORS]=
	Desired_consumption_by_region_and_class[REGION,CLASS]*Share_of_each_sector_in_consumption\
		[REGION,CLASS,SECTORS]
	~	million_euro/Year
	~		|

INITIAL_DEPRECIATION_BY_SECTOR[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_DEPRECIATION_BY_SECTOR'\
		)
	~	
	~		|

CONSUMPTION_PER_CAPITA_2=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_PER_CAPITA_2'\
		)
	~	euro/(person*Year)
	~		|

CONSUMPTION_PER_CAPITA_3=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_PER_CAPITA_3'\
		)
	~	euro/(person*Year)
	~		|

INITIAL_CONSUMPTION_SHARE_1[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_SHARE_1'\
		)
	~	1
	~		|

INITIAL_CONSUMPTION_SHARE_2[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_SHARE_2'\
		)
	~	1
	~		|

INITIAL_CONSUMPTION_SHARE_3[SECTORS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_SHARE_3'\
		)
	~	1
	~		|

Desired_consumption_by_sector[SECTORS]=
	SUM(Desired_consumption_by_region_class_and_sector[REGION!,CLASS!,SECTORS])
	~	million_euro/Year
	~		|

CONSUMPTION_PER_CAPITA_1=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'CONSUMPTION_PER_CAPITA_1'\
		)
	~	euro/(person*Year)
	~		|

I_matrix[SECTORS,SECTORS1]=
	if_then_else(SECTORS=SECTORS1, 1 , 0 )
	~	1
	~		|

SHARE_OF_POPULATION_PER_CLASS[CLASS]=
	0.2,0.5,0.3
	~	
	~		|

INITIAL_CONSUMPTION_PER_CAPITA[REGION,CLASS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_CONSUMPTION_PER_CAPITA'\
		)
	~	euro/(person*Year)
	~		|

CLASS:
	high, medium, low
	~	
	~		|

Leontief_matrix[SECTORS,SECTORS1]=
	INVERT_MATRIX(I_A_matrix[SECTORS,SECTORS1], 25)
	~	1
	~		|

DESIRED_CONSUMPTION_GROWTH_RATE_SP[REGION,CLASS]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'DESIRED_CONSUMPTION_GROWTH_RATE_SP'\
		)
	~	
	~		|

Desired_consumption_per_capita[REGION,CLASS]= INTEG (
	Desired_consumption_per_capita_variation[REGION,CLASS]-Desired_consumption_per_capita_not_covered\
		[REGION,CLASS],
		INITIAL_CONSUMPTION_PER_CAPITA[REGION,CLASS])
	~	euro/(person*Year)
	~		|

Population_by_region_and_class[REGION,CLASS]=
	SUM(Population_in_formal_economy[REGION,AGE_COHORTS!])*SHARE_OF_POPULATION_PER_CLASS\
		[CLASS]
	~	person
	~		|

A_MATRIX_2100[SECTORS, SECTORS1]=
	GET_DIRECT_CONSTANTS('scenario_parameters/scenario_parameters.xlsx' , 'Economy' , 'A_MATRIX_2100'\
		)
	~	1
	~		|

INITIAL_A_MATRIX[SECTORS, SECTORS1]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Economy' , 'INITIAL_A_MATRIX'\
		)
	~	1
	~		|

SECTORS1:
	isengard,
	shire_material,
	m_energy,
	erebor,
	dale,
	dale_re,
	minas_tir,
	m_material,
	lot_alchemy,
	shire_energy,
	gondor,
	lot_ff,
	lot_nuc,
	lot_re_hydro,
	lot_re_wind,
	lot_re_bio,
	lot_re_PV,
	lot_re_stherm,
	lot_re_tide,
	lot_re_gtherm,
	rohan,
	riv_educ,
	riv_health,
	forochel,
	forochel_re
	~	
	~		|

SECTORS:
	isengard,
	shire_material,
	m_energy,
	erebor,
	dale,
	dale_re,
	minas_tir,
	m_material,
	lot_alchemy,
	shire_energy,
	gondor,
	lot_ff,
	lot_nuc,
	lot_re_hydro,
	lot_re_wind,
	lot_re_bio,
	lot_re_PV,
	lot_re_stherm,
	lot_re_tide,
	lot_re_gtherm,
	rohan,
	riv_educ,
	riv_health,
	forochel,
	forochel_re
	~	
	~		|

Birth_rate_formal_economy[REGION,AGE_COHORTS]=
	Birth_rate_over_five_years_formal_economy[REGION,AGE_COHORTS]/5
	~	1/Year
	~		|

Total_population_in_formal_economy_by_region[REGION]=
	SUM(Population_in_formal_economy[REGION,AGE_COHORTS!])
	~	person
	~		|

Births_formal_economy[REGION]=
	SUM(Births_per_age_cohort[REGION,AGE_COHORTS!])
	~	person/Year
	~		|

Mortality_rate_formal_economy[REGION,AGE_COHORTS]=
	Mortality_rate_over_five_years_formal_economy[REGION,AGE_COHORTS]/5
	~	1/Year
	~		|

Deaths_formal_econoy[REGION,AGE_COHORTS]=
	Population_in_formal_economy[REGION,AGE_COHORTS]*Mortality_rate_formal_economy[REGION\
		,AGE_COHORTS]
	~	person/Year
	~		|

FERTILE_AGE:
	C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44
	~	
	~		|

Total_deaths=
	SUM(Total_deaths_by_region[REGION!])
	~	person/Year
	~		|

Total_population_in_formal_economy=
	SUM(Total_population_in_formal_economy_by_region[REGION!])
	~	person
	~		|

Total_deaths_by_region[REGION]=
	SUM(Deaths_formal_econoy[REGION,AGE_COHORTS!])
	~	person/Year
	~		|

UNFERTILE_AGE:
	C_0_4, C_5_9, C_10_14, C_45_49, C_50_54, C_55_59, C_60_64, C_65_69, C_70_74, C_75_79\
		, C_80_84, C_85_89, C_90_94, C_95_plus
	~	
	~		|

Births_per_age_cohort[REGION,AGE_COHORTS]=
	Population_in_formal_economy[REGION,AGE_COHORTS]*Birth_rate_formal_economy[REGION,AGE_COHORTS\
		]
	~	person/Year
	~		|

BETA_1_BIRTH_RATE_S:
	C_30_34,C_35_39
	~	
	~		|

LOG_ALPHA_BIRTH_RATE_S:
	C_15_19,C_20_24
	~	
	~		|

BETA_2_BIRTH_RATE_S:
	C_30_34,C_35_39
	~	
	~		|

Y0_BIRTH_RATE_S:
	C_15_19,C_20_24,C_25_29,C_40_44
	~	
	~		|

ALPHA_BIRTH_RATE_S:
	C_25_29,C_40_44
	~	
	~		|

YF_BIRTH_RATE_S:
	C_15_19,C_20_24,C_25_29,C_40_44
	~	
	~		|

LOG_ALPHA_BIRTH_RATE[LOG_ALPHA_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'LOG_ALPHA_BIRTH_RATE'\
		)
	~	1
	~		|

ALPHA_BIRTH_RATE[ALPHA_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'ALPHA_BIRTH_RATE'\
		)
	~	1
	~		|

BETA_1_BIRTH_RATE[BETA_1_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_1_BIRTH_RATE'\
		)
	~	1
	~		|

BETA_2_BIRTH_RATE[BETA_2_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'BETA_2_BIRTH_RATE'\
		)
	~	1
	~		|

Y0_BIRTH_RATE[Y0_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'Y0_BIRTH_RATE'\
		)
	~	1
	~		|

LOG_ALPHA_MORTALITY_RATE[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'LOG_ALPHA_MORTALITY_RATE'\
		)
	~	1
	~		|

Y0_MORTALITY_RATE[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'Y0_MORTALITY_RATE'\
		)
	~	1
	~		|

YF_BIRTH_RATE[YF_BIRTH_RATE_S]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'YF_BIRTH_RATE'\
		)
	~	1
	~		|

YF_MORTALITY_RATE[AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'YF_MORTALITY_RATE'\
		)
	~	1
	~		|

AGE_COHORTS:
	C_0_4, C_5_9, C_10_14, C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44, C_45_49\
		, C_50_54, C_55_59, C_60_64, C_65_69, C_70_74, C_75_79, C_80_84, C_85_89, C_90_94, \
		C_95_plus
	~	
	~		|

age_middle:
	C_5_9, C_10_14, C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44, C_45_49, C_50_54\
		, C_55_59, C_60_64, C_65_69, C_70_74, C_75_79, C_80_84, C_85_89, C_90_94
	~	
	~		|

age_old:
	C_10_14, C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44, C_45_49, C_50_54, C_55_59\
		, C_60_64, C_65_69, C_70_74, C_75_79, C_80_84, C_85_89, C_90_94, C_95_plus -> age_middle
	~	
	~		|

age_young:
	C_0_4, C_5_9, C_10_14, C_15_19, C_20_24, C_25_29, C_30_34, C_35_39, C_40_44, C_45_49\
		, C_50_54, C_55_59, C_60_64, C_65_69, C_70_74, C_75_79, C_80_84, C_85_89 -> age_middle
	~	
	~		|

INITIAL_POPULATION_IN_FORMAL_ECONOMY[REGION,AGE_COHORTS]=
	GET_DIRECT_CONSTANTS('model_parameters/model_parameters.xlsx' , 'Population' , 'INITIAL_POPULATION_IN_FORMAL_ECONOMY'\
		)
	~	person
	~		|

REGION:
	Centre, Semiperiphery, Periphery -> GOVERNMENT_DEMAND
	~	
	~		|

********************************************************
	.Control
********************************************************~
		Simulation Control Parameters
	|

FINAL_TIME  = 2110
	~	Year
	~	The final time for the simulation.
	|

INITIAL_TIME  = 2019
	~	Year
	~	The initial time for the simulation.
	|

SAVEPER  = 1
	~	Year [0,?]
	~	The frequency with which output is stored.
	|

TIME_STEP  = 0.0078125
	~	Year [0,?]
	~	The time step for the simulation.
	|

\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Demography
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,63,0
10,1,Population in formal economy,1243,509,124,40,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,2,48,928,510,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,3,5,1,4,0,0,22,0,0,0,-1--1--1,,1|(1076,511)|
1,4,5,2,100,0,0,22,0,0,0,-1--1--1,,1|(979,511)|
11,5,0,1027,511,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,6,Births formal economy,1027,528,76,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
12,7,48,1588,505,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,8,10,7,4,0,0,22,0,0,0,-1--1--1,,1|(1539,505)|
1,9,10,1,100,0,0,22,0,0,0,-1--1--1,,1|(1428,505)|
11,10,0,1495,505,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,11,Deaths formal econoy,1495,524,74,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,12,1,11,1,0,0,0,0,128,0,-1--1--1,,1|(1416,541)|
10,13,Birth rate over five years formal economy,823,211,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,14,Mortality rate over five years formal economy,1550,192,106,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,15,INITIAL POPULATION IN FORMAL ECONOMY,1131,422,103,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,16,15,1,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,17,Consumption per capita,1345,57,81,19,8,2,0,3,0,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,18,Government health expenditure per capita,1599,53,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,19,17,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,20,18,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,21,YF MORTALITY RATE,1813,228,78,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,22,Y0 MORTALITY RATE,1818,315,77,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,23,21,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,24,22,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,25,LOG ALPHA MORTALITY RATE,1824,403,94,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,26,25,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,27,YF BIRTH RATE,615,181,64,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,28,Y0 BIRTH RATE,622,228,63,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,29,LOG ALPHA BIRTH RATE,587,275,99,16,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,30,ALPHA BIRTH RATE,604,138,80,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,31,BETA 1 BIRTH RATE,600,95,82,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,32,BETA 2 BIRTH RATE,600,55,82,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,33,Government education expenditure per capita,848,57,78,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,34,29,13,1,0,0,0,0,128,0,-1--1--1,,1|(736,259)|
1,35,28,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,36,27,13,1,0,0,0,0,128,0,-1--1--1,,1|(738,186)|
1,37,30,13,1,0,0,0,0,128,0,-1--1--1,,1|(746,161)|
1,38,31,13,1,0,0,0,0,128,0,-1--1--1,,1|(770,139)|
1,39,32,13,1,0,0,0,0,128,0,-1--1--1,,1|(773,117)|
1,40,33,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,41,17,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,42,Births per age cohort,932,410,73,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,43,1,42,1,0,0,0,0,128,0,-1--1--1,,1|(1027,473)|
1,44,42,5,1,0,0,0,0,128,0,-1--1--1,,1|(965,474)|
10,45,Birth rate formal economy,896,308,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,46,13,45,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,47,45,42,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,48,Mortality rate formal economy,1541,295,85,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,49,14,48,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,50,48,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,51,Total population in formal economy by region,1390,420,107,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,52,1,51,1,0,0,0,0,128,0,-1--1--1,,1|(1360,462)|
10,53,Total population in formal economy,1385,329,92,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,54,51,53,1,0,0,0,0,128,0,-1--1--1,,1|(1399,375)|
10,55,Total deaths by region,1510,580,80,17,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,56,11,55,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,57,Total deaths,1675,580,41,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,58,55,57,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,59,INITIAL POPULATION IN SUBSISTENCE,1028,1075,103,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,60,SHARE OF POPULATION PER CLASS,1187,239,107,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,61,60,14,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,62,SHARE OF POPULATION PER CLASS,1071,60,107,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,63,62,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,64,BETA 0 MORTALITY RATE UNDER SUBSISTENCE,1832,55,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,65,BETA 1 MORTALITY RATE UNDER SUBSISTENCE,1835,152,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,66,64,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,67,65,14,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,68,BETA 0 BIRTH RATE UNDER SUBSISTENCE,604,337,86,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,69,BETA 1 BIRTH RATE UNDER SUBSISTENCE,600,413,90,27,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,70,68,13,1,0,0,0,0,128,0,-1--1--1,,1|(716,308)|
1,71,69,13,1,0,0,0,0,128,0,-1--1--1,,1|(711,364)|
10,72,CONSUMPTION PER CAPITA IN SUBSISTENCE,1204,170,114,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,73,72,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,74,72,14,1,0,0,0,0,128,0,-1--1--1,,1|(1421,163)|
10,75,Government consumption by sector and region,1227,-162,106,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,76,Final demand by components,846,-163,88,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,77,Share of each sector in government consumption,1587,-164,131,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,78,76,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,79,75,33,1,0,0,0,0,128,0,-1--1--1,,1|(1015,-73)|
1,80,75,18,1,0,0,0,0,128,0,-1--1--1,,1|(1524,-22)|
1,81,77,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,82,Total population in formal economy by region,1228,-26,108,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,83,82,33,1,0,0,0,0,128,0,-1--1--1,,1|(1039,-2)|
1,84,82,18,1,0,0,0,0,128,0,-1--1--1,,1|(1443,-3)|
10,85,MATRIX UNITS PREFIXES,1231,-92,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,86,85,33,1,0,0,0,0,128,0,-1--1--1,,1|(1025,-36)|
1,87,85,18,1,0,0,0,0,128,0,-1--1--1,,1|(1417,-48)|
10,88,rate of people that want incorporate to formal economy,1698,709,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,89,BETA 1 SUBSISTENCE TO FORMAL ECONOMY SP,1969,634,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,90,CONSUMPTION PER CAPITA IN SUBSISTENCE,1973,707,112,31,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,91,90,88,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,92,89,88,1,0,0,0,0,128,0,-1--1--1,,1|(1819,666)|
10,93,BETA 0 FORMAL ECONOMY TO SUBSISTENCE SP,537,687,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,94,BETA 1 FORMAL ECONOMY TO SUBSISTENCE SP,527,607,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,95,rate of people that want to incorporate to subsistence,892,696,114,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,96,93,95,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,97,94,95,1,0,0,0,0,128,0,-1--1--1,,1|(756,631)|
10,98,Maximum population in subsistence,510,482,130,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,99,Population in subsistence,1243,919,121,38,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,100,48,931,922,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,101,103,99,4,0,0,22,0,0,0,-1--1--1,,1|(1079,922)|
1,102,103,100,100,0,0,22,0,0,0,-1--1--1,,1|(983,922)|
11,103,0,1031,922,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,104,Births subsistence,1031,941,58,11,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
12,105,48,1577,922,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,106,108,105,4,0,0,22,0,0,0,-1--1--1,,1|(1528,922)|
1,107,108,99,100,0,0,22,0,0,0,-1--1--1,,1|(1421,922)|
11,108,0,1484,922,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,109,Deaths subsistence,1484,941,62,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,110,99,109,1,0,0,0,0,128,0,-1--1--1,,1|(1392,993)|
10,111,Birth rate over five years subsistence,774,908,79,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,112,Births per age cohort subsistence,999,1004,64,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,113,Birth rate subsistence,818,1001,52,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,114,111,113,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,115,113,112,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,116,118,99,4,0,0,22,0,0,0,-1--1--1,,1|(1138,792)|
1,117,118,1,100,0,0,22,0,0,0,-1--1--1,,1|(1138,620)|
11,118,0,1138,697,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,119,Forrmal economy to subsistence,1198,697,52,36,40,131,0,0,-1,0,0,0,0,0,0,0,0,0
1,120,122,1,4,0,0,22,0,0,0,-1--1--1,,1|(1347,626)|
1,121,122,99,100,0,0,22,0,0,0,-1--1--1,,1|(1347,798)|
11,122,0,1347,709,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,123,Subsistence to formal economy,1416,709,61,25,40,131,0,0,-1,0,0,0,0,0,0,0,0,0
10,124,Mortality rate over five years subsistence,1748,906,100,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,125,Mortality rate subsistence,1545,1007,78,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,126,124,125,1,0,0,0,0,128,0,-1--1--1,,1|(1681,986)|
1,127,99,112,1,0,0,0,0,128,0,-1--1--1,,1|(1133,978)|
10,128,YF BIRTH RATE,562,898,82,18,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,129,Y0 BIRTH RATE,574,958,78,17,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,130,LOG ALPHA BIRTH RATE,541,1015,114,18,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,131,ALPHA BIRTH RATE,553,846,96,15,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,132,BETA 1 BIRTH RATE,547,789,98,15,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,133,BETA 2 BIRTH RATE,547,746,98,12,8,130,0,0,0,0,0,0,0,0,0,0,0,0
1,134,133,111,1,0,0,0,0,128,0,-1--1--1,,1|(713,794)|
1,135,132,111,1,0,0,0,0,128,0,-1--1--1,,1|(725,849)|
1,136,131,111,1,0,0,0,0,128,0,-1--1--1,,1|(704,865)|
1,137,128,111,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,138,129,111,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,139,130,111,1,0,0,0,0,128,0,-1--1--1,,1|(716,979)|
10,140,YF MORTALITY RATE,1970,818,104,15,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,141,Y0 MORTALITY RATE,1966,880,94,17,8,130,0,0,0,0,0,0,0,0,0,0,0,0
10,142,LOG ALPHA MORTALITY RATE,2005,946,134,17,8,130,0,0,0,0,0,0,0,0,0,0,0,0
1,143,140,124,1,0,0,0,0,128,0,-1--1--1,,1|(1839,826)|
1,144,141,124,1,0,0,0,0,128,0,-1--1--1,,1|(1839,881)|
1,145,142,124,1,0,0,0,0,128,0,-1--1--1,,1|(1839,941)|
1,146,112,104,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,147,125,109,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,148,CONSUMPTION PER CAPITA IN SUBSISTENCE,1931,1034,76,30,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,149,148,124,1,0,0,0,0,128,0,-1--1--1,,1|(1818,997)|
10,150,CONSUMPTION PER CAPITA IN SUBSISTENCE,534,1078,118,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,151,150,111,1,0,0,0,0,128,0,-1--1--1,,1|(700,1056)|
1,152,59,99,1,0,0,0,0,128,1,-1--1--1,,1|(1138,1027)|
1,153,88,123,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,154,99,123,1,0,0,0,0,128,0,-1--1--1,,1|(1417,823)|
1,155,95,118,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,156,1,119,1,0,0,0,0,128,0,-1--1--1,,1|(1264,605)|
10,157,INITIAL SUBSISTENCE LAND INTENSITY,210,414,139,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,158,Land distribution,280,553,65,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,159,158,98,1,0,0,0,0,128,0,-1--1--1,,1|(388,539)|
1,160,98,118,1,0,0,0,0,128,0,-1--1--1,,1|(948,573)|
1,161,99,119,1,0,0,0,0,128,0,-1--1--1,,1|(1244,812)|
10,162,SHARE OF POPULATION PER CLASS,937,802,150,22,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,163,162,118,1,0,0,0,0,128,0,-1--1--1,,1|(1083,758)|
10,164,Total population in subsistence by region,1448,1073,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,165,99,164,1,0,0,0,0,128,0,-1--1--1,,1|(1317,1025)|
10,166,Total births in subsistence,1006,862,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,167,Total deaths in subsistence,1526,869,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,168,103,166,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,169,108,167,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,170,People that desire to be in subsistence,775,1215,97,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,171,Population in formal economy,675,1294,88,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,172,rate of people that want to incorporate to subsistence,1047,1215,103,22,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,173,Population in subsistence,854,1298,81,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,174,171,170,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,175,173,170,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,176,172,170,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,177,SHARE OF POPULATION PER CLASS,774,1154,107,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,178,177,170,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,179,Delayed TS consumption per capita,551,541,83,23,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,180,Delayed TS consumption per capita,1965,559,87,22,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,181,179,95,1,0,0,0,0,128,0,-1--1--1,,1|(791,598)|
1,182,180,88,1,0,0,0,0,128,0,-1--1--1,,1|(1789,612)|
10,183,Maximum population in subsistence,1701,774,130,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,184,183,123,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,185,Total population in subsistence,1618,1135,59,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,186,164,185,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,187,Average age in formal economy by region,1191,360,97,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,188,1,187,1,0,0,0,0,128,0,-1--1--1,,1|(1270,419)|
10,189,AGE BY COHORT,1162,294,70,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,190,189,187,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,191,Average age in subsistence by region,1238,1076,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,192,AGE BY COHORT,1295,1202,80,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,193,192,191,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,194,99,191,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,195,Total population,1775,1185,53,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,196,Total population in formal economy,1624,1245,75,24,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,197,185,195,1,0,0,0,0,128,0,-1--1--1,,1|(1718,1152)|
1,198,196,195,1,0,0,0,0,128,0,-1--1--1,,1|(1733,1224)|
10,199,Urbanization indicator,1951,1243,72,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,200,ALPHA DEPENDENT POPULATION,1703,1380,134,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,201,ALPHA SUPPORTING INDUSTRY,1711,1444,124,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,202,195,199,1,0,0,0,0,128,0,-1--1--1,,1|(1896,1204)|
1,203,200,199,1,0,0,0,0,128,0,-1--1--1,,1|(1899,1337)|
1,204,201,199,1,0,0,0,0,128,0,-1--1--1,,1|(1919,1386)|
1,205,185,199,1,0,0,0,0,128,0,-1--1--1,,1|(1853,1153)|
10,206,Workers,1791,1313,38,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,207,206,199,1,0,0,0,0,128,0,-1--1--1,,1|(1897,1290)|
10,208,Subsistence land intensity,192,328,83,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-192-0,0,0,0,0,0,0
1,209,208,98,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Economy
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,73,0
10,1,INITIAL A MATRIX,2062,-816,75,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,2,A matrix before application of factors,2256,-685,78,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,3,A MATRIX 2100,2442,-816,63,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,4,1,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,5,INITIAL TIME,2070,-692,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,6,5,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,7,I A matrix,2260,-573,37,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,8,I matrix,2432,-574,27,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,9,8,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,10,Leontief matrix,2260,-474,49,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,11,7,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,12,Desired consumption per capita,809,350,75,26,3,131,0,0,0,0,0,0,0,0,0,0,0,0
10,13,Desired consumption by region and class,1168,-23,101,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,14,Population in formal economy,534,28,43,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
12,15,48,522,348,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,16,18,12,4,0,0,22,0,0,0,-1--1--1,,1|(686,348)|
1,17,18,15,100,0,0,22,0,0,0,-1--1--1,,1|(579,348)|
11,18,0,633,348,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,19,Desired consumption per capita variation,633,375,101,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
12,20,48,1101,350,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,21,23,20,4,0,0,22,0,0,0,-1--1--1,,1|(1044,350)|
1,22,23,12,100,0,0,22,0,0,0,-1--1--1,,1|(935,350)|
11,23,0,992,350,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,24,Desired consumption per capita not covered,992,377,103,19,40,131,0,0,-1,0,0,0,0,0,0,0,0,0
1,25,12,13,1,0,0,0,0,128,0,-1--1--1,,1|(978,210)|
10,26,DESIRED CONSUMPTION GROWTH RATE SP,404,201,114,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,27,12,19,1,0,0,0,0,128,0,-1--1--1,,1|(754,422)|
10,28,INITIAL CONSUMPTION PER CAPITA,749,464,104,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,29,28,12,1,0,0,0,0,128,1,-1--1--1,,1|(795,421)|
10,30,SHARE OF POPULATION PER CLASS,788,28,142,13,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,31,Population by region and class,788,199,66,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,32,14,31,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,33,30,31,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,34,31,13,1,0,0,0,0,128,0,-1--1--1,,1|(971,122)|
10,35,Share of each sector in consumption,1691,221,74,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,36,CONSUMPTION PER CAPITA 1,1417,95,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,37,INITIAL CONSUMPTION SHARE 1,1492,536,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,38,INITIAL CONSUMPTION SHARE 2,1923,535,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,39,INITIAL CONSUMPTION SHARE 3,2055,195,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,40,CONSUMPTION PER CAPITA 2,1419,355,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,41,CONSUMPTION PER CAPITA 3,1833,93,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,42,12,35,1,0,0,0,0,128,0,-1--1--1,,1|(1234,234)|
10,43,Desired consumption by region class and sector,1438,-224,85,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,44,Desired consumption by sector,1697,-223,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,45,Desired government consumption by sector,1701,-398,102,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,46,43,44,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,47,Desired final demand by sector,1986,-398,87,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,48,45,47,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,49,44,47,1,0,0,0,0,128,0,-1--1--1,,1|(1854,-285)|
10,50,Desired consumption by region,1090,-222,88,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,51,Desired government consumption by region,1127,-399,102,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,52,Desired government consumption by sector and region,1416,-398,114,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,53,51,52,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,54,52,45,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,55,50,51,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,56,35,43,1,0,0,0,0,128,0,-1--1--1,,1|(1570,37)|
10,57,Share of each sector in government consumption,1228,-513,107,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,58,57,52,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,59,13,43,1,0,0,0,0,128,0,-1--1--1,,1|(1304,-112)|
10,60,Desired output by sector,2261,-397,78,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,61,47,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,62,10,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,63,Desired gross fixed capital formation by sector,2151,-221,103,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,64,Output by sector,2547,-397,57,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,65,Scarcity factor,3125,-289,48,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,66,65,64,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,67,60,64,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,68,Capital stock,2729,347,105,30,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,69,48,3116,347,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,70,72,69,4,0,0,22,0,0,0,-1--1--1,,1|(3041,347)|
1,71,72,68,100,0,0,22,0,0,0,-1--1--1,,1|(2899,347)|
11,72,0,2970,347,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,73,Depreciation by sector,2970,366,77,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,74,Delayed time step output by sector,2938,-219,94,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,75,Capital intensity before damage,3070,23,89,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,76,INITIAL CAPITAL INTENSITY,3309,107,91,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,77,CAPITAL INTENSITY 2100 SP,3306,-59,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,78,64,74,1,0,0,0,0,128,0,-1--1--1,,1|(2774,-310)|
10,79,Share of each sector in gfcf,2381,-224,56,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,80,Desired investment by sector,2607,35,98,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,81,68,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,82,72,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,83,INITIAL DEPRECIATION BY SECTOR,2771,606,137,14,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,84,79,63,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,85,Scarcitiy factor for investment,2293,213,85,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,86,Initial capital stock,2556,437,64,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,87,86,68,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,88,68,73,1,0,0,0,0,128,0,-1--1--1,,1|(2869,394)|
10,89,INITIAL TIME,3512,24,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,90,INITIAL OUTPUT,3124,-159,66,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,91,90,74,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,92,TIME STEP,2937,-156,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,93,92,74,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,94,GOVERNMENT CONSUMPTION AS SHARE OF HOUSEHOLDS CONSUMPTION BY REGION,723,-399,191,28,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,95,Desired consumption per capita by region,396,-196,101,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,96,12,95,1,0,0,0,0,128,0,-1--1--1,,1|(472,94)|
1,97,30,95,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,98,3,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,99,Consumption per capita,962,455,80,9,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,100,Final demand,1830,-653,45,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,101,Scarcity factor,1752,-554,57,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,102,Final demand by sector,1940,-489,74,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,103,101,102,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,104,47,102,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,105,102,100,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,106,31,50,1,0,0,0,0,128,0,-1--1--1,,1|(1002,5)|
1,107,95,50,1,0,0,0,0,128,0,-1--1--1,,1|(799,-117)|
10,108,Final demand by components,1738,-789,83,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,109,100,108,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,110,Desired consumption by region and class,1212,-723,102,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,111,Desired gross fixed capital formation,2192,29,77,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,112,63,111,1,0,0,0,0,128,0,-1--1--1,,1|(2215,-97)|
10,113,Desired gross fixed capital formation,1208,-793,99,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,114,Desired government consumption by region,1212,-867,105,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,115,Demand priority vector,1900,-883,78,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,116,115,108,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,117,Desired final demand by components,1520,-791,95,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,118,114,117,1,0,0,0,0,128,0,-1--1--1,,1|(1392,-850)|
1,119,113,117,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,120,110,117,1,0,0,0,0,128,0,-1--1--1,,1|(1403,-733)|
1,121,117,108,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,122,PTYPE DEMAND MP,1569,-968,86,16,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,123,PPRIORITY DEMAND MP,1781,-967,113,17,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,124,PWIDTH DEMAND MP,1999,-968,91,16,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,125,PEXTRA DEMAND MP,2215,-967,94,17,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,126,122,115,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,127,123,115,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,128,124,115,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,129,125,115,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
12,130,48,2314,345,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,131,133,68,4,0,0,22,0,0,0,-1--1--1,,1|(2554,345)|
1,132,133,130,100,0,0,22,0,0,0,-1--1--1,,1|(2398,345)|
11,133,0,2478,345,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,134,Investment by sector,2478,362,70,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,135,85,133,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,136,80,133,1,0,0,0,0,128,0,-1--1--1,,1|(2567,218)|
10,137,Final demand by components,2034,28,69,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,138,111,85,1,0,0,0,0,128,0,-1--1--1,,1|(2223,123)|
1,139,137,85,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,140,Final demand by components,1225,456,115,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,141,140,99,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,142,MATRIX UNITS PREFIXES,1166,-133,86,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,143,MATRIX UNITS PREFIXES,962,531,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,144,143,99,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,145,142,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,146,142,50,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,147,Population by region and class,1229,530,115,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,148,147,99,1,0,0,0,0,128,0,-1--1--1,,1|(1077,501)|
1,149,99,24,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,150,12,24,1,0,0,0,0,64,0,-1--1--1,,1|(894,412)|
10,151,A matrix damage factor,2644,-875,74,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,152,Total output,2470,-351,41,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,153,64,152,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,154,Final demand as share of output,1672,-652,65,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,155,100,154,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,156,Labour scarcity factor,3307,-298,84,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,157,156,65,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,158,Target growth rate A matrix,2257,-767,60,25,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,159,1,158,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,160,3,158,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,161,INITIAL TIME,2255,-853,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,162,161,158,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,163,158,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,164,Time,2118,-736,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,165,164,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,166,Mortality scarcity factor,3305,-254,94,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,167,Mortality rate formal economy,3302,-111,66,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,168,166,65,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,169,Delayed time step mortality rate,3304,-181,89,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,170,167,169,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,171,169,166,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,172,TIME STEP,3492,-181,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,173,172,169,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,174,Desired final demand,1670,-506,71,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,175,47,174,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,176,Desired consumption,1698,-157,69,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,177,44,176,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,178,Desired government consumption,1616,-313,89,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,179,45,178,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,180,INITIAL OUTPUT,2349,436,75,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,181,INITIAL CAPITAL INTENSITY,2304,499,120,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,182,180,86,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,183,181,86,1,0,0,0,0,128,0,-1--1--1,,1|(2487,480)|
10,184,Depreciation rate,2811,437,56,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,185,86,184,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,186,83,184,1,0,0,0,0,128,0,-1--1--1,,1|(2794,527)|
1,187,184,73,1,0,0,0,0,128,0,-1--1--1,,1|(2950,394)|
10,188,Capital intensity,2825,-19,52,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,189,75,188,1,0,0,0,0,128,0,-1--1--1,,1|(2937,15)|
1,190,188,80,1,0,0,0,0,128,0,-1--1--1,,1|(2687,36)|
10,191,OUTPUT LOSSES FACTOR SP,3114,150,92,19,8,131,0,0,-1,0,0,0,0,0,0,0,0,0
10,192,Temperature change base 1850,2991,261,91,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,193,Depreciation rate caused by climate change,3058,449,103,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,194,193,73,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,195,SECTORAL SHARES OF DAMAGES IN CAPITAL STOCK SP,2971,549,137,27,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,196,195,193,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,197,Temperature change base 1850,3220,553,91,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,198,197,193,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,199,Extraction difficulty factor,2781,-971,63,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,200,199,151,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
10,201,Temperature change base 1850,3076,-763,91,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,202,Total output,1503,-655,50,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,203,202,154,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,204,Fossil fuels rationing scarcity factor,3362,-342,133,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,205,204,65,1,0,0,0,0,128,0,-1--1--1,,1|(3197,-330)|
10,206,Accumulated depreciation rate caused by sea level rise 2°C,3759,247,115,42,3,131,0,0,0,0,0,0,0,0,0,0,0,0
10,207,Accumulated depreciation rate caused by sea level rise 3°C,3746,407,115,42,3,131,0,0,0,0,0,0,0,0,0,0,0,0
10,208,Accumulated depreciation rate caused by sea level rise 4°C,3748,566,115,42,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,209,48,3396,245,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,210,212,206,4,0,0,22,0,0,0,-1--1--1,,1|(3587,245)|
1,211,212,209,100,0,0,22,0,0,0,-1--1--1,,1|(3462,245)|
11,212,0,3525,245,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,213,Depreciation rate caused by sea level rise 2°C,3525,272,106,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
12,214,48,3377,405,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,215,217,207,4,0,0,22,0,0,0,-1--1--1,,1|(3571,406)|
1,216,217,214,100,0,0,22,0,0,0,-1--1--1,,1|(3443,406)|
11,217,0,3506,406,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,218,Depreciation rate caused by sea level rise 3°C,3506,433,106,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
12,219,48,3379,571,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,220,222,208,4,0,0,22,0,0,0,-1--1--1,,1|(3573,571)|
1,221,222,219,100,0,0,22,0,0,0,-1--1--1,,1|(3445,571)|
11,222,0,3508,571,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,223,Depreciation rate caused by sea level rise 4°C,3508,598,106,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,224,Depreciation rate caused by sea level rise,3237,344,82,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,225,213,224,1,0,0,0,0,128,0,-1--1--1,,1|(3363,304)|
1,226,218,224,1,0,0,0,0,128,0,-1--1--1,,1|(3373,428)|
1,227,222,224,1,0,0,0,0,128,0,-1--1--1,,1|(3358,509)|
1,228,224,72,1,0,0,0,0,128,0,-1--1--1,,1|(3060,302)|
1,229,80,63,1,0,0,0,0,128,0,-1--1--1,,1|(2405,-58)|
10,230,Accumulated extra GFCF due to sea level rise,1712,-70,83,47,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,231,48,2019,-75,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,232,234,230,4,0,0,22,0,0,0,-1--1--1,,1|(1849,-75)|
1,233,234,231,100,0,0,22,0,0,0,-1--1--1,,1|(1962,-75)|
11,234,0,1909,-75,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,235,Extra GFCF due to sea level rise,1909,-45,93,19,40,131,0,0,-1,0,0,0,0,0,0,0,0,0
10,236,TOTAL EXTRA GFCF DUE TO SEA LEVEL RISE SP,1921,-220,118,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,237,236,234,1,0,0,0,0,128,0,-1--1--1,,1|(1927,-137)|
10,238,Threshold of 2°C exceeded,1822,27,99,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,239,238,235,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,240,230,235,1,0,0,0,0,128,0,-1--1--1,,1|(1819,-10)|
1,241,234,63,1,0,0,0,0,128,0,-1--1--1,,1|(2021,-137)|
1,242,63,47,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,243,Year threshold of 2°C exceeded,3470,164,120,15,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,244,Year threshold of 3°C exceeded,3488,329,119,14,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,245,Year threshold of 4°C exceeded,3500,482,117,17,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,246,243,212,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,247,244,217,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,248,245,222,1,0,0,0,0,128,0,-1--1--1,,1|(3514,523)|
10,249,Time,3544,203,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,250,Time,3543,362,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,251,249,212,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,252,250,217,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,253,Time,3471,528,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,254,253,222,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,255,74,80,1,0,0,0,0,128,0,-1--1--1,,1|(2755,-121)|
10,256,Total initial output,3126,-228,60,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,257,90,256,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,258,Total capital stock,2729,405,63,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,259,68,258,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,260,Land scarcity factor,3055,-344,77,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,261,260,65,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,262,ALPHA OUTPUT LOSSES A MATRIX SP,3123,-970,151,16,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,263,BETA OUTPUT LOSSES A MATRIX SP,3118,-903,147,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,264,GAMMA OUTPUT LOSSES A MATRIX SP,3131,-828,156,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,265,Delayed TS consumption per capita,753,530,93,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,266,28,265,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,267,99,265,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,268,TIME STEP,776,610,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,269,268,265,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,270,94,51,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,271,Extraction difficulty factor,3089,-96,91,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,272,271,188,1,0,0,0,0,128,0,-1--1--1,,1|(2929,-80)|
10,273,Target capital intensity growth rate,3289,25,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,274,89,273,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,275,77,273,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,276,76,273,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,277,76,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,278,77,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,279,273,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,280,INITIAL TIME,3069,104,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,281,280,75,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,282,Time,3186,101,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,283,282,75,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,284,Output losses due to climate change,2866,106,94,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,285,191,284,1,0,0,0,0,128,0,-1--1--1,,1|(2971,145)|
1,286,192,284,1,0,0,0,0,128,0,-1--1--1,,1|(2921,201)|
1,287,284,188,1,0,0,0,0,128,0,-1--1--1,,1|(2835,43)|
10,288,Output losses factor A matrix,2831,-869,59,26,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,289,262,288,1,0,0,0,0,128,0,-1--1--1,,1|(2902,-936)|
1,290,263,288,1,0,0,0,0,128,0,-1--1--1,,1|(2913,-892)|
1,291,264,288,1,0,0,0,0,128,0,-1--1--1,,1|(2913,-838)|
1,292,201,288,1,0,0,0,0,128,0,-1--1--1,,1|(2922,-778)|
1,293,288,151,1,0,0,0,0,128,0,-1--1--1,,1|(2730,-839)|
10,294,MAXIMUM DEPRECIATION RATE CAUSED BY SEA LEVEL RISE 2°C SP,3755,160,149,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,295,MAXIMUM DEPRECIATION RATE CAUSED BY SEA LEVEL RISE 3°C SP,3771,326,148,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,296,MAXIMUM DEPRECIATION RATE CAUSED BY SEA LEVEL RISE 4°C SP,3771,481,149,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,297,SIGMA SLR SP,3411,362,58,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,298,294,212,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,299,295,217,1,0,0,0,0,128,0,-1--1--1,,1|(3596,368)|
1,300,296,222,1,0,0,0,0,128,0,-1--1--1,,1|(3608,519)|
10,301,SIGMA SLR SP,3716,646,66,11,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,302,SIGMA SLR SP,3410,208,66,11,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
1,303,302,212,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,304,301,223,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,305,297,217,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,306,TARGET CONSUMPTION SHARE 1,1703,538,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,307,TARGET CONSUMPTION SHARE 2,2058,420,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,308,TARGET CONSUMPTION SHARE 3,2058,319,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,309,41,35,1,0,0,0,0,128,0,-1--1--1,,1|(1780,162)|
1,310,36,35,1,0,0,0,0,128,0,-1--1--1,,1|(1526,159)|
1,311,40,35,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,312,Consumption share 1,1562,421,72,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,313,Consumption share 2,1800,421,72,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,314,Consumption share 3,1894,244,72,9,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,315,37,312,1,0,0,0,0,128,0,-1--1--1,,1|(1516,469)|
1,316,306,312,1,0,0,0,0,128,0,-1--1--1,,1|(1646,468)|
1,317,38,313,1,0,0,0,0,128,0,-1--1--1,,1|(1877,472)|
1,318,307,313,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,319,39,314,1,0,0,0,0,128,0,-1--1--1,,1|(1943,209)|
1,320,308,314,1,0,0,0,0,128,0,-1--1--1,,1|(1948,288)|
1,321,312,35,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,322,313,35,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,323,314,35,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,324,INITIAL TIME,1387,419,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,325,324,312,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,326,INITIAL TIME,2026,470,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,327,326,313,1,0,0,0,0,64,0,-1--1--1,,1|(1912,449)|
10,328,INITIAL TIME,2049,243,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,329,328,314,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,330,SWITCH DEPRECIATION RATE CAUSED BY CLIMATE CHANGE SP,3120,614,149,27,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,331,330,193,1,0,0,0,0,128,0,-1--1--1,,1|(3112,530)|
10,332,SWITCH DAMAGES SEA LEVEL RISE SP,3246,254,104,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,333,332,224,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,334,SWITCH DAMAGES SEA LEVEL RISE SP,2106,-117,86,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,335,334,234,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,336,SWITCH OUTPUT LOSS FACTOR SP,3074,207,75,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,337,336,284,1,0,0,0,0,128,0,-1--1--1,,1|(2950,174)|
10,338,SWITCH OUTPUT LOSS FACTOR SP,2746,-767,102,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,339,338,288,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,340,ratio capital output,2519,607,64,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,341,Output by sector,2382,653,68,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,342,Capital stock,2375,574,53,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,343,342,340,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,344,341,340,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,345,ratio capital output total economy,2217,607,66,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,346,342,345,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,347,341,345,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,348,INITIAL CAPITAL FACTOR TO ADJUST INVESTMENTS,2617,505,124,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,349,INVESTMENT SPEED PARAMETER,2377,30,101,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,350,TARGET EXCESS CAPACITY OF THE CAPITAL STOCK,2386,110,121,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,351,349,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,352,350,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,353,348,86,1,0,0,0,0,128,0,-1--1--1,,1|(2573,468)|
10,354,SSP sectors variation factor,2650,-625,59,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,355,BETA 1 SSP,2838,-700,47,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,356,BETA 2 SSP,2841,-644,47,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,357,BETA 3 SSP,2840,-586,47,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,358,Total population,2754,-398,64,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,359,Output per capita by sector,2648,-452,58,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,360,64,359,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,361,358,359,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,362,SWITCH SSP SECTORS VARIATION FACTOR,2880,-520,90,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,363,355,354,1,0,0,0,0,128,0,-1--1--1,,1|(2732,-684)|
1,364,356,354,1,0,0,0,0,128,0,-1--1--1,,1|(2753,-640)|
1,365,357,354,1,0,0,0,0,128,0,-1--1--1,,1|(2752,-591)|
1,366,362,354,1,0,0,0,0,128,0,-1--1--1,,1|(2737,-547)|
10,367,Delayed TS output per capita by sector,2613,-541,58,31,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,368,359,367,1,0,0,0,0,128,0,-1--1--1,,1|(2630,-482)|
1,369,367,354,1,0,0,0,0,128,0,-1--1--1,,1|(2624,-582)|
10,370,INITIAL OUTPUT,2923,-398,75,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,371,INITIAL POPULATION IN FORMAL ECONOMY,3131,-392,108,21,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,372,Initial output per capita,2903,-456,79,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,373,370,372,1,0,0,0,0,128,0,-1--1--1,,1|(2914,-418)|
1,374,371,372,1,0,0,0,0,128,0,-1--1--1,,1|(3004,-423)|
1,375,372,367,1,0,0,0,0,128,1,-1--1--1,,1|(2760,-479)|
10,376,INITIAL POPULATION IN SUBSISTENCE,3132,-471,94,23,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,377,376,372,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,378,TIME STEP,2481,-461,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,379,378,367,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,380,A matrix,2258,-624,30,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,381,2,380,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,382,380,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,383,151,380,1,0,0,0,0,128,0,-1--1--1,,1|(2481,-708)|
1,384,354,380,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,385,Mortality scarcity factor,1477,-505,90,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,386,Mortality scarcity factor,2261,-322,90,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,387,386,47,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,388,Mortality scarcity factor,2518,-68,56,24,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,389,388,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,390,Desired consumption growth rate,528,276,48,32,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,391,390,18,1,0,0,0,0,128,0,-1--1--1,,1|(600,310)|
1,392,26,390,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,393,Growth slowdown,296,417,61,9,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,394,Growth slowdown fossil fuels rationing factor,86,521,72,28,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,395,Growth slowdown labour factor,247,522,73,26,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,396,Growth slowdown land rationing factor,397,517,59,31,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,397,394,393,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,398,395,393,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,399,396,393,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,400,Growth slowdown factor,373,326,55,31,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,401,393,400,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,402,400,390,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,403,SWITCH GROWTH SLOWDOWN SP,151,326,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,404,403,400,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,405,INITIAL SHARE OF EACH SECTOR IN GROSS FIXED CAPITAL FOMATION,2602,-276,106,30,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,406,TARGET SHARE OF EACH SECTOR IN GROSS FIXED CAPITAL FOMATION SP,2609,-158,110,31,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,407,406,79,1,0,0,0,0,128,0,-1--1--1,,1|(2480,-164)|
1,408,405,79,1,0,0,0,0,128,0,-1--1--1,,1|(2454,-264)|
10,409,INITIAL TIME,2565,-222,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,410,409,79,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,411,INITIAL SHARE OF EACH SECTOR IN GOVERNMENT CONSUMPTION,1098,-636,141,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,412,TARGET SHARE OF EACH SECTOR IN GOVERNMENT CONSUMPTION SP,866,-530,148,24,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,413,411,57,1,0,0,0,0,128,0,-1--1--1,,1|(1171,-583)|
1,414,412,57,1,0,0,0,0,128,0,-1--1--1,,1|(1068,-540)|
10,415,INITIAL TIME,1060,-456,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,416,415,57,1,0,0,0,0,64,0,-1--1--1,,1|(1134,-474)|
10,417,Growth slowdown factor climate damages in labor intensity,488,429,118,19,8,3,0,2,0,0,0,0,-1--1--1,0-0-0,|||255-128-0,0,0,0,0,0,0
10,418,Growth slowdown labour damage factor,562,503,102,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,419,418,417,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,420,417,400,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Labour
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,90,0
10,1,Labour demand,552,456,52,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,2,Labour intensity before damage,545,224,86,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,3,INITIAL LABOUR INTENSITY,371,71,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,4,Maximum labour supply,979,166,81,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,5,Population in formal economy,887,70,60,17,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,6,ANNUAL WORKING HOURS SP,1104,66,119,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,7,5,4,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,8,6,4,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,9,Labour scarcity factor,1202,345,74,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,10,Workforce utilization rate,980,265,79,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,11,4,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,12,10,9,1,0,0,0,0,128,0,-1--1--1,,1|(1074,332)|
10,13,Desired output by sector,372,453,66,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,14,MATRIX UNITS PREFIXES,550,538,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,15,14,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,16,Total labour demand,758,458,70,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,17,1,16,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,18,16,10,1,0,0,0,0,128,0,-1--1--1,,1|(923,334)|
1,19,13,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,20,TARGET LABOUR INTENSITY SP,716,71,97,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,21,Labour intensity growth rate,543,121,55,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,22,3,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,23,20,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,24,INITIAL TIME,542,61,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,25,24,21,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,26,3,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,27,20,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,28,INITIAL TIME,754,224,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,29,28,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,30,Time,394,221,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,31,30,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,32,21,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,33,Temperature change base 1850,1349,271,121,12,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,34,MAXIMUM PARTICIPATION RATE SP,1277,114,141,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,35,34,4,1,0,0,0,0,128,0,-1--1--1,,1|(1053,131)|
10,36,ALPHA DAMAGE LABOUR SUPPLY SP,1377,169,146,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,37,Labour intensity,549,300,52,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,38,2,37,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,39,37,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,40,ALPHA DAMAGE LABOUR PRODUCTIVITY SP,201,245,112,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,41,Temperature change base 1850,203,299,115,12,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,42,Extraction difficulty factor,767,364,94,15,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,43,42,37,1,0,0,0,0,128,0,-1--1--1,,1|(631,346)|
10,44,Output losses due to climate change,345,369,99,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,45,44,37,1,0,0,0,0,128,0,-1--1--1,,1|(482,348)|
10,46,Damages on labour productivity produced by heat,410,287,62,26,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,47,40,46,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,48,41,46,1,0,0,0,0,128,0,-1--1--1,,1|(326,298)|
1,49,46,37,1,0,0,0,0,128,0,-1--1--1,,1|(498,281)|
10,50,Losses of maximum labour supply due to heat,1143,214,106,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,51,36,50,1,0,0,0,0,128,0,-1--1--1,,1|(1196,182)|
1,52,33,50,1,0,0,0,0,128,0,-1--1--1,,1|(1196,246)|
1,53,50,4,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,54,SWITCH LABOUR SCARCITY FACTOR,1201,467,103,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,55,54,9,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,56,SWITCH DAMAGES ON LABOUR PRODUCTIVITY BY HEAT SP,236,156,134,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,57,56,46,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,58,SWITCH LOSSES LABOUR SUPPLY BY HEAT SP,1386,216,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,59,58,50,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,60,Real labour,755,525,39,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,61,Total real labour,905,525,56,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,62,1,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,63,60,61,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,64,Scarcity factor,642,584,57,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,65,64,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,66,Workers,795,582,29,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,67,60,66,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,68,ANNUAL WORKING HOURS SP,690,625,132,15,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,69,68,66,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,70,Total workers,932,583,47,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,71,66,70,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,72,Growth slowdown labour factor,1031,390,64,16,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,73,10,72,1,0,0,0,0,128,0,-1--1--1,,1|(994,319)|
1,74,54,72,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,75,output losses due to climate change isengard,186,449,104,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,76,Output losses due to climate change,223,445,99,19,8,2,1,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,77,44,75,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,78,Damages on labour productivity isengard,54,348,100,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,79,46,78,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,80,added climate damage on labor intensity isengard,36,405,108,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,81,78,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,82,75,80,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,83,Growth slowdown labour damage factor,98,512,97,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,84,80,83,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Energy
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,69,0
10,1,CONVERSION FACTOR MONETARY TO ENERGY,556,37,115,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,2,CONVERSION FACTOR MONETARY TO NON ENERGY USE OF FOSSIL FUELS,554,370,164,24,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,3,Desired final energy by sector and type,556,146,100,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,4,Desired non energy use of fossil fuels,554,294,97,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,5,1,3,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,6,2,4,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,7,Desired final energy resources used by type,749,210,102,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,8,3,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,9,4,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,10,Desired primary energy of fossil fuels by type,1004,373,107,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,11,7,10,1,0,0,0,0,128,0,-1--1--1,,1|(834,308)|
10,12,Desired primary energy of uranium,1000,117,93,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,13,3,12,1,0,0,0,0,128,0,-1--1--1,,1|(774,120)|
10,14,CONVERSION FROM FINAL ENERGY TO PRIMARY ENERGY URANIUM,998,39,146,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,15,CONVERSION FROM FINAL ENERGY TO PRIMARY ENERGY FOSSIL FUELS,1023,214,149,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,16,14,12,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,17,15,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,18,Recoverable resources of fossil fuels,899,614,76,29,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,19,48,899,812,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,20,22,19,4,0,0,22,0,0,0,-1--1--1,,1|(899,766)|
1,21,22,18,100,0,0,22,0,0,0,-1--1--1,,1|(899,680)|
11,22,0,899,723,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,23,Fossil fuel depletion,974,723,67,9,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,24,INITIAL RECOVERABLE RESOURCES OF FOSSIL FUELS SP,1216,729,139,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,25,24,18,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,26,Extraction difficulty factor,1138,614,79,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,27,BETA 0 EXTRACTION SP,1485,715,95,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,28,BETA 1 EXTRACTION SP,1473,614,94,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,29,18,26,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,30,27,26,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,31,28,26,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,32,24,26,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,33,Desired output by sector,355,219,83,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,34,33,3,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,35,33,4,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,36,Final energy use by sector and type,384,485,95,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,37,Final non energy use fossil fuels,390,578,90,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,38,Final energy use and non energy use of resources,387,662,112,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,39,Primary energy of uranium,396,743,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,40,Primary energy of fossil fuels by type,400,845,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,41,Desired final energy by sector and type,611,488,100,19,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,42,Desired non energy use of fossil fuels,621,577,97,19,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,43,Desired final energy resources used by type,615,662,93,19,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,44,Desired primary energy of fossil fuels by type,400,929,107,19,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,45,Desired primary energy of uranium,614,742,77,24,8,130,0,2,0,0,0,0,-1--1--1,0-0-0,|||128-128-128,0,0,0,0,0,0
10,46,Scarcity factor,138,662,57,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,47,41,36,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,48,42,37,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,49,43,38,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,50,45,39,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,51,44,40,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,52,46,36,1,0,0,0,0,128,0,-1--1--1,,1|(207,543)|
1,53,46,37,1,0,0,0,0,128,0,-1--1--1,,1|(218,609)|
1,54,46,38,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,55,46,39,1,0,0,0,0,128,0,-1--1--1,,1|(241,719)|
1,56,46,40,1,0,0,0,0,128,0,-1--1--1,,1|(223,787)|
1,57,40,22,1,0,0,0,0,128,0,-1--1--1,,1|(693,834)|
10,58,Fossil fuels rationing scarcity factor,1339,467,93,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,59,MAXIMUM SHARE OF EXTRACTABLE FOSSIL FUEL RESOURCES PER YEAR SP,1369,273,165,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,60,18,58,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,61,10,58,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,62,59,58,1,0,0,0,0,128,0,-1--1--1,,1|(1359,368)|
10,63,SWITCH FOSSIL FUELS EXTRACTION DIFFICULTY FACTOR SP,1515,538,150,31,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,64,63,26,1,0,0,0,0,128,0,-1--1--1,,1|(1294,568)|
10,65,SWITCH FOSSIL FUELS RATIONING SCARCITY FACTOR,1534,368,128,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,66,65,58,1,0,0,0,0,128,0,-1--1--1,,1|(1456,424)|
10,67,Growth slowdown fossil fuels rationing factor,1406,121,84,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,68,59,67,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,69,65,67,1,0,0,0,0,128,0,-1--1--1,,1|(1563,290)|
10,70,Recoverable resources of fossil fuels,1647,120,79,24,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,71,70,67,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,72,10,67,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Land
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,60,0
10,1,Land distribution,1639,273,55,11,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,2,INITIAL UNUSED FOREST,1901,125,108,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,3,Land demand,985,273,46,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,4,3,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,5,Disposable land,1338,393,52,11,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,6,5,1,1,0,0,0,0,128,0,-1--1--1,,1|(1591,311)|
1,7,5,3,1,0,0,0,0,128,0,-1--1--1,,1|(1141,357)|
10,8,Land demand for human use,891,447,102,14,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,9,Sectorial land demand,731,362,75,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,10,Foodland demand for subsistence,677,447,66,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,11,10,8,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,12,Infraestructure demand,738,527,75,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,13,12,8,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,14,Desired output by sector,559,316,98,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,15,Sectorial land intensities before damage,730,162,98,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,16,14,9,1,0,0,0,0,128,0,-1--1--1,,1|(642,345)|
10,17,INITIAL SUBSISTENCE LAND INTENSITY,-42,280,90,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,18,INFRAESTRUCTURE LAND INTENSITY,711,637,154,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,19,18,12,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,20,Desired consumption,460,635,79,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,21,20,12,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,22,9,8,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,23,8,3,1,0,0,0,0,128,0,-1--1--1,,1|(917,361)|
10,24,Foodland and forest priority vector,1920,544,131,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,25,PTYPE LAND SP,1766,631,39,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,26,PPRIORITY LAND SP,1880,630,43,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,27,PWIDTH LAND SP,1992,630,49,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,28,PEXTRA LAND SP,2117,630,49,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,29,25,24,1,0,0,0,0,128,0,-1--1--1,,1|(1830,578)|
1,30,26,24,1,0,0,0,0,128,0,-1--1--1,,1|(1900,581)|
1,31,27,24,1,0,0,0,0,128,0,-1--1--1,,1|(1981,567)|
1,32,28,24,1,0,0,0,0,128,0,-1--1--1,,1|(2079,585)|
1,33,24,1,1,0,0,0,0,128,0,-1--1--1,,1|(1772,443)|
10,34,INITIAL SECTORIAL LANDS INTENSITIES,535,-44,105,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,35,TARGET LAND INTENSITIES SP,927,-49,94,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,36,34,15,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,37,35,15,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,38,Land intensity growth rate,728,14,64,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,39,34,38,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,40,35,38,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,41,38,15,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,42,INITIAL TIME,728,-50,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,43,42,38,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,44,INITIAL TIME,549,116,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,45,44,15,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,46,Time,546,60,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,47,46,15,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,48,Delayed land distribution,1965,454,75,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,49,1,48,1,0,0,0,0,128,0,-1--1--1,,1|(1765,380)|
10,50,Land variation,2175,453,47,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,51,1,50,1,0,0,0,0,128,0,-1--1--1,,1|(1919,388)|
1,52,48,50,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,53,Land generating emissions increase,2176,554,69,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,54,50,53,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,55,Sectorial land intensities,730,263,80,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,56,15,55,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,57,55,9,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,58,INITIAL DISPOSABLE LAND,987,535,116,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,59,58,5,1,0,0,0,0,128,0,-1--1--1,,1|(1130,500)|
10,60,Land loss caused by climate change,1223,537,94,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,61,Foodland loss caused by climate change,1545,537,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,62,MAXIMUM LAND LOSS CAUSED BY CLIMATE CHANGE SP,1019,643,130,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,63,MAXIMUM FOODLAND LOSS CAUSED BY CLIMATE CHANGE SP,1541,645,141,29,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,64,62,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,65,63,61,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,66,Temperature change base 1850,1382,497,47,30,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,67,66,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,68,66,61,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,69,60,5,1,0,0,0,0,128,0,-1--1--1,,1|(1297,476)|
1,70,61,5,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,71,Delayed TS unused forest,1738,67,96,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,72,1,71,1,0,0,0,0,128,0,-1--1--1,,1|(1713,184)|
1,73,2,71,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,74,71,3,1,0,0,0,0,128,0,-1--1--1,,1|(1322,56)|
10,75,TIME STEP,1933,68,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,76,75,71,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,77,Delayed TS used forest,1376,199,87,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,78,1,77,1,0,0,0,0,128,0,-1--1--1,,1|(1580,241)|
1,79,77,3,1,0,0,0,0,128,0,-1--1--1,,1|(1168,215)|
10,80,INITIAL USED FOREST,1520,143,92,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,81,80,77,1,0,0,0,0,128,1,-1--1--1,,1|(1449,168)|
10,82,TIME STEP,1376,236,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,83,82,77,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,84,Forest land reduction,2332,495,69,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,85,50,84,1,0,0,0,0,128,0,-1--1--1,,1|(2281,470)|
10,86,Land use change generating emissions,2311,622,83,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,87,53,86,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,88,84,86,1,0,0,0,0,128,0,-1--1--1,,1|(2333,563)|
10,89,Sectorial lands scarcity factor,2082,35,71,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,90,3,89,1,0,0,0,0,128,0,-1--1--1,,1|(1184,70)|
1,91,1,89,1,0,0,0,0,128,0,-1--1--1,,1|(2048,129)|
10,92,Land scarcity factor,2141,205,68,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,93,89,92,1,0,0,0,0,128,0,-1--1--1,,1|(2120,117)|
10,94,ALPHA LAND SUBSISTENCE DAMAGE SP,20,640,161,17,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,95,Temperature change base 1850,-22,542,121,18,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,96,People that desire to be in subsistence,495,537,85,23,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,97,96,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,98,Output losses due to climate change,553,214,99,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,99,98,55,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,100,TARGET SUBSISTENCE LAND INTENSITY SP,-39,455,110,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,101,INITIAL TIME,-44,366,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,102,Subsistence land intensity growth rate,128,363,77,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,103,Subsistence land intensity before damage,334,366,98,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,104,Subsistence land intensity,428,446,79,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,105,100,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,106,17,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,107,17,102,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,108,100,102,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,109,101,102,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,110,102,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,111,103,104,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,112,104,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,113,INITIAL TIME,154,466,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,114,113,103,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,115,Time,290,466,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,116,115,103,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,117,Extra subsistence land intensity due to climate damage,266,543,72,34,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,118,95,117,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,119,94,117,1,0,0,0,0,128,0,-1--1--1,,1|(184,606)|
1,120,117,104,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,121,SWITCH LAND SCARCITY FACTOR SP,2081,312,91,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,122,121,92,1,0,0,0,0,128,0,-1--1--1,,1|(2119,261)|
10,123,SWITCH LAND LOSS CAUSED BY CLIMATE CHANGE SP,1275,644,124,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,124,123,60,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,125,123,61,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,126,SWITCH SUBSISTENCE LAND INTENSITY DUE TO CLIMATE CHANGE SP,266,753,169,32,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,127,126,117,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,128,PPRIORIY PROTECTION LAND SP,1933,711,56,30,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,129,AMOUNT OF LAND TO PROTECT,2071,714,53,30,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,130,129,24,1,0,0,0,0,128,0,-1--1--1,,1|(2057,618)|
1,131,128,24,1,0,0,0,0,128,0,-1--1--1,,1|(1940,627)|
10,132,Delayed TS land distribution,1646,453,85,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,133,5,132,1,0,0,0,0,128,1,-1--1--1,,1|(1475,437)|
1,134,1,132,1,0,0,0,0,128,0,-1--1--1,,1|(1624,353)|
1,135,132,24,1,0,0,0,0,128,0,-1--1--1,,1|(1725,502)|
10,136,TIME STEP,1541,393,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,137,136,132,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,138,Land demand,696,727,55,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,139,Growth slowdown land rationing factor,879,768,74,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,140,138,139,1,0,0,0,0,128,0,-1--1--1,,1|(785,731)|
10,141,Disposable land,698,812,62,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,142,141,139,1,0,0,0,0,128,0,-1--1--1,,1|(785,806)|
10,143,SWITCH LAND SCARCITY FACTOR SP,1106,768,99,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,144,143,139,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Stressors
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,70,0
10,1,INITIAL GREENHOUSE GAS EMISSIONS INTENSITY,404,119,117,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,2,Output by sector,800,384,47,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,3,Greenhouse gas emissions,946,306,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,4,2,3,1,0,0,0,0,128,0,-1--1--1,,1|(885,349)|
10,5,LAND USE CHANGE EMISSIONS INTENSITY,714,621,96,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,6,Land use change emissions by land,980,597,73,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,7,5,6,1,0,0,0,0,128,0,-1--1--1,,1|(867,624)|
10,8,MATERIAL EXTRACTION INTENSITY USED,2010,250,110,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,9,Output by sector,2036,424,52,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,10,MATERIAL EXTRACTION INTENSITY UNUSED,2019,589,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,11,Material extraction used,2249,306,94,15,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,12,8,11,1,0,0,0,0,128,0,-1--1--1,,1|(2191,273)|
1,13,9,11,1,0,0,0,0,128,0,-1--1--1,,1|(2087,349)|
10,14,Material extracción unused,2262,527,102,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,15,9,14,1,0,0,0,0,128,0,-1--1--1,,1|(2152,526)|
1,16,10,14,1,0,0,0,0,128,0,-1--1--1,,1|(2203,575)|
10,17,Material extraction for renewables,2525,234,89,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,18,Total material extraction,2527,373,81,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,19,11,18,1,0,0,0,0,128,0,-1--1--1,,1|(2360,360)|
1,20,11,17,1,0,0,0,0,128,0,-1--1--1,,1|(2353,250)|
10,21,INDUSTRIAL ROUNDWOOD INTENSITY,2272,1371,59,31,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,22,Output by sector,2262,1251,46,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,23,Industrial roundwood,2491,1311,70,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,24,22,23,1,0,0,0,0,128,0,-1--1--1,,1|(2398,1268)|
1,25,21,23,1,0,0,0,0,128,0,-1--1--1,,1|(2402,1350)|
10,26,INITIAL WATER CONSUMPTION INDUSTRIAL INTENSITY,390,699,127,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,27,Output by sector,816,889,73,16,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,28,Water industrial consumption,951,826,85,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,29,27,28,1,0,0,0,0,128,0,-1--1--1,,1|(868,860)|
10,30,INITIAL WATER WITHDRAWAL INDUSTRIAL INTENSITY,380,951,114,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,31,Water industrial withdrawal,949,956,80,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,32,27,31,1,0,0,0,0,128,0,-1--1--1,,1|(867,920)|
10,33,INITIAL WATER CONSUMPTION INTENSITY OF HOUSEHOLDS,601,1155,127,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,34,INITIAL WATER WITHDRAWAL INTENSITY OF HOUSEHOLD,588,1360,129,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,35,Final demand by components,804,1301,66,19,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,36,Water consumption of households,945,1245,68,23,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,37,35,36,1,0,0,0,0,128,0,-1--1--1,,1|(888,1286)|
10,38,Water withdrawal intensity of households,946,1365,78,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,39,35,38,1,0,0,0,0,128,0,-1--1--1,,1|(887,1321)|
10,40,Water use by type,1120,1064,65,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,41,Water use,1272,1065,35,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,42,28,40,1,0,0,0,0,128,0,-1--1--1,,1|(1098,936)|
1,43,31,40,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,44,36,40,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,45,38,40,1,0,0,0,0,128,0,-1--1--1,,1|(1095,1225)|
1,46,40,41,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,47,INITIAL NITROGEN AND PHOSPHORUS POLLUTION INTENSITY OF AGRICULTURE,1835,669,169,28,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,48,Output by sector,2132,930,49,34,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,49,INITIAL AIR POLLUTION SECTORIAL INTENSITY,1974,1018,99,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,50,Nitrogen and phosphurus pollution of agriculture,2498,853,106,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,51,Air pollution,2473,1023,41,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,52,48,50,1,0,0,0,0,128,0,-1--1--1,,1|(2318,907)|
1,53,48,51,1,0,0,0,0,128,0,-1--1--1,,1|(2318,943)|
10,54,Anthropogenic HFC Emissions,948,108,87,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,55,3,54,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,56,Anthropogenic CH4 Emissions,1221,101,84,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,57,Anthropogenic CO2 Emissions wo LUC,1217,209,99,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,58,Anthropogenic N2O Emissions,1227,305,87,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,59,Anthropogenic SF6 Emissions,1235,399,84,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,60,Anthropogenic PFC Emissions,1234,499,86,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,61,Anthropogenic LUC CO2 Emissions,1241,601,92,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,62,3,56,1,0,0,0,0,0,0,-1--1--1,,1|(1066,164)|
1,63,3,57,1,0,0,0,0,64,0,-1--1--1,,1|(1067,242)|
1,64,3,58,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,65,3,59,1,0,0,0,0,64,0,-1--1--1,,1|(1082,363)|
1,66,3,60,1,0,0,0,0,64,0,-1--1--1,,1|(1050,415)|
1,67,6,61,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,68,FOSSIL FUEL EMISSIONS INTENSITY,1599,172,172,23,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,69,CO2 from fossil energy combustion,1708,279,86,23,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,70,68,69,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,71,69,57,1,0,0,0,0,192,0,-1--1--1,,1|(1469,227)|
10,72,CONVERSION FROM FINAL ENERGY TO PRIMARY ENERGY FOSSIL FUELS,1636,447,296,14,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,73,72,69,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,74,Final energy use by sector and type,1534,347,93,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,75,74,69,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,76,Land use change generating emissions,727,557,81,21,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,77,76,6,1,0,0,0,0,64,0,-1--1--1,,1|(860,566)|
10,78,CORRECTION P SOIL,2142,854,98,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,79,78,50,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,80,CORRECTION CHEMICAL AND FERTILIZER MINERALS,2248,157,122,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,81,80,11,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,82,Total air polution,2701,1024,57,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,83,51,82,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,84,Greenhouse gas emissions intensity before climate damage,563,191,106,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,85,1,84,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,86,TARGET GREENHOUSE GAS EMISSIONS INTENSITY,404,276,119,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,87,86,84,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,88,Water consumption industrial intensity before climate damage,611,752,105,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,89,TARGET WATER CONSUMPTION INDUSTRIAL INTENSITY SP,394,811,129,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,90,26,88,1,0,0,0,0,128,0,-1--1--1,,1|(550,708)|
1,91,89,88,1,0,0,0,0,128,0,-1--1--1,,1|(561,796)|
10,92,TARGET WATER WITHDRAWAL INDUSTRIAL INTENSITY SP,364,1075,123,22,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,93,Water withdrawal industrial intensity before climate damage,614,1015,107,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,94,30,93,1,0,0,0,0,128,0,-1--1--1,,1|(539,969)|
1,95,92,93,1,0,0,0,0,128,0,-1--1--1,,1|(542,1067)|
10,96,TARGET WATER CONSUMPTION INTENSITY OF HOUSEHOLDS SP,591,1263,135,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,97,Water consumption intensity of households,788,1209,75,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,98,33,97,1,0,0,0,0,128,0,-1--1--1,,1|(750,1170)|
1,99,96,97,1,0,0,0,0,128,0,-1--1--1,,1|(748,1248)|
10,100,TARGET WATER WITHDRAWAL INTENSITY OF HOUSEHOLD SP,583,1479,131,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,101,Water withdrawal intensity of household,782,1417,73,20,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,102,34,101,1,0,0,0,0,128,0,-1--1--1,,1|(732,1371)|
1,103,100,101,1,0,0,0,0,128,0,-1--1--1,,1|(743,1457)|
1,104,101,38,1,0,0,0,0,128,0,-1--1--1,,1|(890,1410)|
1,105,97,36,1,0,0,0,0,128,0,-1--1--1,,1|(878,1210)|
10,106,TARGET NITROGEN AND PHOSPHORUS POLLUTION INTENSITY OF AGRICULTURE SP,1830,787,182,25,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,107,Nitrogen and phosphorus pollution intensity of agriculture before damages,2121,730,134,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,108,47,107,1,0,0,0,0,128,0,-1--1--1,,1|(2046,688)|
1,109,106,107,1,0,0,0,0,128,0,-1--1--1,,1|(2043,777)|
10,110,TARGET AIR POLLUTION SECTORIAL INTENSITY SP,1972,1137,108,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,111,Air pollution sectorial intensity before damages,2171,1077,82,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,112,49,111,1,0,0,0,0,128,0,-1--1--1,,1|(2102,1036)|
1,113,110,111,1,0,0,0,0,128,0,-1--1--1,,1|(2116,1120)|
10,114,Greenhouse gas emissions intensity growth rate,365,191,64,26,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,115,1,114,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,116,86,114,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,117,114,84,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,118,Water consumption industrial intensity growth rate,361,755,108,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,119,118,88,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,120,Water withdrawal industrial intensity growth rate,352,1013,106,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,121,Water consumption intensity of households growth rate,592,1209,95,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,122,30,120,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,123,92,120,1,0,0,0,0,128,0,-1--1--1,,1|(368,1060)|
1,124,120,93,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,125,33,121,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,126,96,121,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,127,121,97,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,128,Water withdrawal intensity of household growth rate,579,1418,111,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,129,34,128,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,130,100,128,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,131,128,101,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,132,Nitrogen and phosphorus pollution intensity of agriculture growth rate,1831,724,131,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,133,47,132,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,134,106,132,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,135,132,107,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,136,Air pollution sectorial intensity growth rate,1971,1078,75,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,137,49,136,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,138,110,136,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,139,136,111,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,140,INITIAL TIME,204,191,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,141,140,114,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,142,26,118,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,143,89,118,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,144,INITIAL TIME,167,755,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,145,144,118,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,146,INITIAL TIME,164,1010,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,147,146,120,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,148,INITIAL TIME,402,1210,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,149,148,121,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,150,INITIAL TIME,384,1415,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,151,150,128,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,152,INITIAL TIME,1603,723,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,153,152,132,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,154,INITIAL TIME,1795,1077,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,155,154,136,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,156,Greenhouse gas emissions intensity,773,192,70,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,157,84,156,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,158,156,3,1,0,0,0,0,128,0,-1--1--1,,1|(876,239)|
10,159,Water consumption industrial intensity,820,753,71,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,160,88,159,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,161,159,28,1,0,0,0,0,128,0,-1--1--1,,1|(909,777)|
10,162,Water withdrawal industrial intensity,815,1016,65,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,163,162,31,1,0,0,0,0,128,0,-1--1--1,,1|(907,1003)|
1,164,93,162,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,165,Nitrogen and phosphorus pollution intensity of agriculture,2396,732,105,18,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,166,107,165,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,167,165,50,1,0,0,0,0,128,0,-1--1--1,,1|(2464,780)|
10,168,Air pollution sectorial intensity,2387,1080,62,21,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,169,168,51,1,0,0,0,0,128,0,-1--1--1,,1|(2453,1056)|
1,170,111,168,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,171,Output losses due to climate change,652,276,71,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,172,171,156,1,0,0,0,0,128,0,-1--1--1,,1|(719,241)|
10,173,Output losses due to climate change,634,892,71,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,174,Output losses due to climate change,2226,666,71,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,175,Output losses due to climate change,2255,1142,71,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,176,174,165,1,0,0,0,0,128,0,-1--1--1,,1|(2341,689)|
1,177,175,168,1,0,0,0,0,128,0,-1--1--1,,1|(2354,1129)|
1,178,173,159,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,179,173,162,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,180,INITIAL TIME,672,110,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,181,180,84,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,182,Time,557,110,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,183,182,84,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,184,INITIAL TIME,744,690,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,185,184,88,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,186,Time,617,691,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,187,186,88,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,188,INITIAL TIME,686,1081,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,189,188,93,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,190,Time,575,1084,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,191,190,93,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,192,INITIAL TIME,880,1145,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,193,192,97,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,194,Time,779,1146,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,195,194,97,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,196,INITIAL TIME,874,1470,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,197,196,101,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,198,Time,776,1472,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,199,198,101,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,200,INITIAL TIME,2201,783,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,201,200,107,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,202,Time,2097,784,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,203,202,107,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,204,INITIAL TIME,2247,1011,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,205,204,111,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,206,Time,2138,1011,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,207,206,111,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Planetary boundaries
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,60,0
10,1,PBI Climate CO2 concentration,160,171,89,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,2,PBI Climate CO2 radiative forcing,951,174,93,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,3,PBI biosphere integrity,2196,174,77,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,4,PBI ozone,2663,176,36,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,5,PBI ocean acidification,148,476,78,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,6,PBI biogeochemical flows phosphurus,959,478,95,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,7,PBI land system change,1761,175,75,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,8,PBI freshwater blue water,664,836,81,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,9,PBI freshwater green water,1123,836,82,19,8,131,0,0,0,0,0,0,0,0,0,0,0,0
10,10,PBI aerosol loading,2725,512,67,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,11,PBI novel entities,2062,864,59,11,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,12,Initial atmospheric concentrations CO2,-55,220,89,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,13,Initial effective Radiative Forcing,723,251,84,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,14,12,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,15,13,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,16,Land distribution,1980,117,65,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,17,Initial land distribution,1982,231,73,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,18,16,17,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,19,16,3,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,20,17,3,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,21,WEIGHTS FOR LAND SYSTEM CHANGE,2141,53,108,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,22,21,3,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,23,Aragonite saturation,-49,416,75,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,24,Initial aragonite saturation,-46,535,77,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,25,23,5,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,26,24,5,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,27,23,24,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,28,Nitrogen and phosphurus pollution of agriculture,734,414,112,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,29,Initial nitrogen and phosphurus pollution of agriculture,734,544,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,30,28,6,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,31,29,6,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,32,28,29,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,33,PBI biogeochemical flows nitrogen,2059,502,91,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,34,16,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,35,17,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,36,atmospheric concentrations CO2,-55,102,74,24,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,37,36,12,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,38,36,1,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,39,Effective Radiative Forcing,721,105,85,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,40,39,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,41,39,13,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,42,Material extraction used,1834,403,96,17,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,43,Initial material extraction used,1833,577,85,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,44,42,43,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,45,42,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,46,43,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,47,Water industrial consumption,765,686,85,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,48,Water consumption of households,997,689,95,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,49,Water consumption,882,767,65,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,50,47,49,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,51,48,49,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,52,Initial water consumption,884,909,75,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,53,49,52,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,54,49,9,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,55,52,9,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,56,49,8,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,57,52,8,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,58,Total air polution,2525,407,68,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,59,Initial total air polution,2527,587,77,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,60,58,59,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,61,58,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,62,59,10,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,63,Output by sector,1836,780,68,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,64,initial output by sector,1835,931,76,9,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,65,63,11,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,66,64,11,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,67,63,64,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,68,Upper threshold PBI Climate CO2 concentration,376,105,109,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,69,Lower threshold PBI Climate CO2 concentration,380,230,109,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,70,Upper threshold PBI Climate CO2 radiative forcing,1198,105,109,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,71,Lower threshold PBI Climate CO2 radiative forcing,1205,248,109,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,72,Upper threshold PBI biosphere integrity,2389,112,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,73,Lower threshold PBI biosphere integrity,2399,247,96,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,74,Upper threshold PBI ozone,2798,108,82,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,75,Lower threshold PBI ozone,2789,250,83,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,76,Upper threshold PBI ocean acidification,369,419,98,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,77,Lower threshold PBI ocean acidification,370,545,98,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,78,Upper threshold PBI biogeochemical flows phosphurus,1217,403,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,79,Lower threshold PBI biogeochemical flows phosphurus,1220,540,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,80,Upper threshold PBI biogeochemical flows nitrogen,2237,410,113,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,81,Lower threshold PBI biogeochemical flows nitrogen,2236,577,108,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,82,Upper threshold PBI novel entities,2223,785,92,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,83,Lower threshold PBI novel entities,2215,933,92,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,84,Upper threshold PBI land system change,1551,111,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,85,Lower threshold PBI land system change,1548,253,99,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Exogenous variables
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,100,0
10,1,Initial cumulative CO2 emissions,1344,-830,111,27,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,2,0,1342,-888,101,24,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - Total GHG emissions
10,3,GWP 100 year,1345,-789,55,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,4,GWP 20 year,1347,-756,51,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,5,Biomass Res Time,1043,-830,68,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,6,0,1043,-881,86,21,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - CARBON CYCLE
10,7,Biostimulation coeff index,1043,-798,95,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,8,Biostimulation coeff mean,1047,-767,95,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,9,Buff C Coeff,1033,-732,47,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,10,CH4 Generation Rate from Biomass,1023,-698,115,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,11,CH4 Generation Rate from Humus,1026,-653,113,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,12,Eddy diff coeff index,1022,-548,78,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,13,Eddy diff mean,1012,-519,55,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,14,Humification Fraction,1016,-455,78,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,15,Humus Res Time,1011,-422,63,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,16,Init C in Biomass,1006,-396,66,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,17,Init C in Deep Ocean per meter,998,-360,110,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,18,Init C in Humus,1000,-322,61,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,19,Init C in Mixed Ocean per meter,1000,-286,114,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,20,init CO2 in atmosphere ppm,993,-239,107,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,21,Init NPP,990,-203,32,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,22,Layer Depth,989,-177,44,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,23,Mixed Depth,987,-149,46,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,24,Mixing Time,988,-122,45,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,25,pre industrial ppm CO2,981,-48,88,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,26,Preind Ocean C per meter,981,4,98,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,27,Preindustrial C,977,49,53,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,28,Ref Buffer Factor,975,83,65,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,29,Reference Temperature Change for Effect of Warming on CH4 from Respiration,987,129,174,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,30,SWITCH Sensitivity of C Uptake to Temperature,1033,219,137,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,31,SWITCH Sensitivity of Methane Emissions to Temperature,1025,281,148,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,32,Sensitivity of pCO2 DIC to Temperature Mean,1034,354,132,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,33,Strength of temp effect on land C flux mean,1046,415,130,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,34,CF4 molar mass,750,-836,59,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,35,0,760,-883,99,26,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - OTHER GHG CYCLES
10,36,CH4 molar mass,749,-808,62,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,37,HFC molar mass,721,-401,61,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,38,HFC radiative efficiency,730,-359,86,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,39,Init PFC in Atm con,723,-314,78,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,40,Inital HFC con,716,-279,53,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,41,Initial CH4 conc,718,-251,59,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,42,Initial N2O conc,710,-214,61,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,43,Initial SF6 con,712,-182,54,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,44,N2O N molar mass,707,-142,73,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,45,Natural N2O emissions,706,-102,85,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,46,PFC radiative efficiency,705,-53,85,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,47,Preindustrial CH4,698,46,65,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,48,Preindustrial HFC conc,696,78,84,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,49,Preindustrial PFC conc,696,126,83,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,50,Preindustrial SF6 conc,690,163,83,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,51,Reference CH4 time constant,683,205,108,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,52,Reference Sensitivity of CH4 from Permafrost and Clathrate to Temperature SP,624,318,174,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,53,SWITCH Sensitivity of Methane Emissions to Permafrost and Clathrate,682,386,164,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,54,SF6 molar mass,672,426,59,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,55,SF6 radiative efficiency,674,459,85,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,56,Stratospheric CH4 path share,672,504,110,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,57,Temperature Threshold for Methane Emissions from Permafrost and Clathrate SP,660,559,175,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,58,Time Const for HFC,658,618,76,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,59,Time Const for N2O,665,659,78,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,60,Time Const for PFC,665,706,75,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,61,Time Const for SF6,657,749,75,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,62,Tropospheric CH4 path share,657,821,108,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,63,CH4 N20 inter exp,413,-842,73,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,64,0,410,-888,102,26,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - RADIACTIVE FORCING
10,65,CH4 N20 inter exp 2,416,-806,82,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,66,CH4 N2O inter coef 2,408,-770,86,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,67,CH4 N2O inter coef 3,408,-730,86,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,68,CH4 N2O interaction coeffient,386,-687,106,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,69,CH4 N2O unit adj,383,-642,70,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,70,CH4 radiative efficiency coefficient,381,-604,114,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,71,CH4 reference conc,375,-555,72,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,72,CO2 Rad Force coefficient,371,-514,97,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,73,N2O radiative efficiency coefficient,365,-346,115,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,74,N2O reference conc,361,-305,73,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,75,Time to Commit RF,352,-180,74,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,76,0,111,-891,92,30,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - TEMPERATURE CHANGE
10,77,global surface area,92,-786,69,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,78,Heat Diffusion Covar,70,-630,77,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,79,Heat Transfer Rate,66,-588,70,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,80,init Atmos UOcean Temp,64,-553,94,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,81,Init Deep Ocean Temp,59,-505,83,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,82,land area fraction,64,-460,65,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,83,land thickness,67,-422,51,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,84,pH constant 1,1336,-593,54,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,85,pH constant 2,1333,-559,54,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,86,pH constant 3,1329,-531,54,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,87,pH constant 4,1328,-499,54,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,88,0,1333,-639,78,19,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - PH
12,89,0,1328,-444,82,26,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) CLIMATE - SEA-LEVEL RISE
10,90,initial sea level rise in 2019,1332,-330,107,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,91,Reference Temperature,1327,-279,82,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,92,Sensitivity of Sea Level Rise to Temperature,1322,-183,131,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,93,Sensitivity of SLR rate to temp rate,1306,-136,119,27,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,94,Temp Adjustment for SLR,1306,-50,97,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,95,0,-219,-898,92,30,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
(CLI) Historic emissions
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Constants
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,100,0
12,1,0,612,-45,92,23,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
UNIT CONVERSION
10,2,C PER CO2,600,575,44,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,3,DAYS PER YEAR,614,60,65,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,4,PERCENT TO SHARE,863,250,80,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,5,0,626,-123,171,25,8,135,0,40,-1,0,0,0,-1--1--1,0-0-0,Dubai|16||0-0-0,0,0,0,0,0,0
Constants and units conversion
10,6,MATRIX UNIT PREFIXES,291,132,91,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,7,WATT PER J s,601,682,58,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,8,SECONDS PER YEAR,614,116,80,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,9,WATER DENSITY,615,736,66,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,10,SPECIFIC HEAT CAPACITY WATER,615,810,117,27,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,11,CH4 PER C,606,634,44,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,12,ppt PER MOL,888,392,52,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,13,ppt PER ppb,889,422,48,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,14,INITIAL SIMULATION YEAR,293,373,103,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Carboncycle
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,68,0
12,1,0,949,-169,103,28,3,135,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
C-ROADS subclimate model (adapted from MEDEAS-W 2.0
10,2,atmospheric concentrations CO2,1110,184,107,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,3,0,1484,-186,57,19,0,7,0,56,0,0,0,0,-1--1--1,0-0-0,Dubai|16|I|0-0-0,0,0,0,0,0,0
Carbon cycle
10,4,C in Atmosphere,1400,417,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,5,48,1065,405,1,1,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,6,C PER CO2,786,267,53,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,7,init C in atmosphere,1336,348,77,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,8,4,2,1,0,0,0,0,64,0,-1--1--1,,1|(1184,304)|
10,9,C in Humus,1386,60,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,10,12,4,4,0,0,22,0,0,0,-1--1--1,,1|(1379,303)|
1,11,12,9,100,0,0,22,0,0,0,-1--1--1,,1|(1379,139)|
11,12,0,1379,204,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,13,Flux Humus to Atmosphere,1472,204,102,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,14,Humus Res Time,1528,117,72,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,15,14,13,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,16,9,13,1,0,0,0,0,128,0,-1--1--1,,1|(1455,98)|
10,17,Init C in Humus,1189,110,71,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,18,C in Biomass,1732,365,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,19,21,9,4,0,0,22,0,0,0,-1--1--1,,1|(1506,45)|
1,20,21,18,100,0,0,22,0,0,0,-1--1--1,,1|(1732,45)|
11,21,0,1593,45,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,22,Flux Biomass to Humus,1593,71,89,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,23,Humification Fraction,1576,165,87,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,24,Biomass Res Time,1648,200,77,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,25,Init C in Biomass,1642,318,75,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,26,18,22,1,0,0,0,0,128,0,-1--1--1,,1|(1677,197)|
1,27,23,22,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,28,24,22,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,29,31,4,4,0,0,22,0,0,0,-1--1--1,,1|(1400,316)|
1,30,31,18,100,0,0,22,0,0,0,-1--1--1,,1|(1525,365)|
11,31,0,1525,316,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,32,Flux Biomass to Atmosphere,1525,342,106,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,33,23,31,1,0,0,0,0,128,0,-1--1--1,,1|(1558,243)|
1,34,24,31,1,0,0,0,0,128,0,-1--1--1,,1|(1594,266)|
1,35,18,32,1,0,0,0,0,128,0,-1--1--1,,1|(1658,373)|
1,36,38,18,4,0,0,22,0,0,0,-1--1--1,,1|(1732,404)|
1,37,38,4,100,0,0,22,0,0,0,-1--1--1,,1|(1501,404)|
11,38,0,1568,404,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,39,Flux Atm to Biomass,1568,430,80,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,40,4,39,1,0,0,0,0,128,0,-1--1--1,,1|(1493,456)|
10,41,Preindustrial C,1606,485,64,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,42,41,39,1,0,0,0,0,128,0,-1--1--1,,1|(1565,486)|
10,43,Biostimulation coeff,1727,487,72,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,44,43,39,1,0,0,0,0,128,0,-1--1--1,,1|(1637,468)|
10,45,Biostimulation coeff index,1904,462,104,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,46,Biostimulation coeff mean,1893,494,104,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,47,45,43,1,0,0,0,0,128,1,-1--1--1,,1|(1777,464)|
1,48,46,43,1,0,0,0,0,128,1,-1--1--1,,1|(1783,502)|
10,49,Init NPP,1754,424,41,15,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,50,49,39,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,51,Effect of Warming on C flux to biomass,1948,416,125,27,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,52,51,39,1,0,0,0,0,128,0,-1--1--1,,1|(1748,451)|
1,53,7,4,1,0,0,0,0,64,1,-1--1--1,,1|(1348,380)|
10,54,Strength of Temp Effect on C Flux to Land,2198,359,129,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,55,Strength of temp effect on land C flux mean,2253,229,134,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,56,SWITCH Sensitivity of C Uptake to Temperature,2211,455,127,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,57,54,51,1,0,0,0,0,128,0,-1--1--1,,1|(2055,381)|
1,58,25,18,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1673,320)|
1,59,17,9,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1253,72)|
1,60,55,54,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(2259,283)|
1,61,56,54,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(2168,348)|
10,62,C in Mixed Layer,1419,655,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,63,C in Deep Ocean,1428,986,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,64,66,62,4,0,0,22,0,0,0,-1--1--1,,1|(1416,591)|
1,65,66,4,68,0,0,22,2,0,0,-1--1--1,|||0-0-0,1|(1416,486)|
11,66,0,1416,542,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,67,Flux Atm to Ocean,1499,542,72,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,68,70,63,4,0,0,22,0,0,0,-1--1--1,,1|(1415,886)|
1,69,70,62,100,0,0,22,0,0,0,-1--1--1,,1|(1415,735)|
11,70,0,1415,801,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,71,Diffusion Flux,1474,801,50,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,72,Equil C in Mixed Layer,1616,541,86,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,73,Effect of Temp on DIC pCO2,1807,543,110,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,74,Sensitivity of pCO2 DIC to Temperature,2066,592,121,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,75,Sensitivity of pCO2 DIC to Temperature Mean,2151,674,136,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,76,Buffer Factor,1621,606,48,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,77,Mixing Time,1507,601,54,15,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,78,Preind C in Mixed Layer,1838,606,91,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,79,Buff C Coeff,1748,639,56,15,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,80,Ref Buffer Factor,1751,677,74,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,81,Init C in Mixed Ocean per meter,1663,706,115,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,82,C in mixed layer per meter,1468,722,102,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,83,Mixed Depth,1691,764,55,15,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,84,Equil C in Mixed Layer,1865,763,96,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,85,Equilibrium C per meter in Mixed Layer,1867,944,121,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,86,C in deep ocean per meter,1482,869,101,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,87,Layer Depth,1595,941,53,15,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,88,Mean Depth of Adjacent Layers,1655,862,110,27,8,131,0,32,0,0,0,0,-1--1--1,-1--1--1,Dubai|||0-0-0,0,0,0,0,0,0
10,89,Init C in Deep Ocean per meter,1649,1055,115,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,90,62,67,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1445,612)|
1,91,77,67,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,92,72,67,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1591,555)|
1,93,41,72,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1617,503)|
1,94,4,72,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1491,496)|
1,95,76,72,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1607,575)|
1,96,73,72,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,97,78,72,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,98,78,76,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,99,79,76,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,100,80,76,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1673,642)|
1,101,74,73,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,102,56,74,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(2170,515)|
1,103,75,74,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(2047,602)|
10,104,Preind Ocean C per meter,1949,687,107,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,105,104,78,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1906,607)|
1,106,83,78,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1810,711)|
1,107,81,62,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,108,83,62,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,109,83,88,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1697,793)|
1,110,83,85,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1768,813)|
1,111,84,85,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,112,88,71,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,113,82,71,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1475,739)|
1,114,62,82,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,115,86,71,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1468,840)|
1,116,63,86,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1475,947)|
1,117,87,86,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,118,89,63,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1518,1034)|
1,119,87,63,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1509,989)|
1,120,87,88,1,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(1632,907)|
1,121,62,76,0,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(0,0)|
1,122,83,82,1,0,0,0,1,128,0,0-0-255,|||0-0-0,1|(1571,757)|
10,123,Eddy diff coeff,1285,797,54,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,124,Eddy diff coeff index,1257,695,87,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,125,Eddy diff mean,1278,872,66,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,126,Layer Time Constant,1090,780,76,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,127,Mean Depth of Adjacent Layers,904,864,115,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,128,Layer Depth,1129,849,53,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,129,123,126,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,130,125,123,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,131,124,123,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,132,128,126,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,133,127,126,0,0,0,0,2,128,1,-1--1--1,|||0-0-0,1|(0,0)|
1,134,123,70,0,0,0,0,2,128,0,-1--1--1,|||0-0-0,1|(0,0)|
10,135,Flux Biosphere to CH4,1848,33,85,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,136,CH4 Generation Rate from Biomass,2001,313,119,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,137,CH4 Generation Rate from Humus,1820,-55,118,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,138,SWITCH Sensitivity of Methane Emissions to Temperature,1291,-208,138,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,139,Effect of Warming on CH4 Release from Biological Activity,1467,-95,146,27,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,140,138,139,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,141,Reference Temperature Change for Effect of Warming on CH4 from Respiration,1776,-213,171,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,142,141,139,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,143,Effect of Warming on CH4 Release from Biological Activity,1965,210,150,27,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
12,144,48,1385,-66,25,15,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,145,147,144,4,0,0,22,0,0,0,-1--1--1,,1|(1385,-30)|
1,146,147,9,100,0,0,22,0,0,0,-1--1--1,,1|(1385,21)|
11,147,0,1385,-3,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,148,Flux Humus to CH4,1471,-3,75,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,149,137,148,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,150,148,135,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,151,9,147,1,0,0,0,0,128,0,-1--1--1,,1|(1348,20)|
1,152,139,148,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,153,MATRIX UNIT PREFIXES,2049,-67,100,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,154,CH4 PER C,2041,126,53,15,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
12,155,48,1923,364,25,15,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,156,158,155,4,0,0,22,0,0,0,-1--1--1,,1|(1873,364)|
1,157,158,18,100,0,0,22,0,0,0,-1--1--1,,1|(1804,364)|
11,158,0,1842,364,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,159,Flux Biomass to CH4,1842,390,80,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,160,136,158,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,161,143,158,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,162,158,135,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,163,18,158,1,0,0,0,0,128,0,-1--1--1,,1|(1792,322)|
10,164,Natural CH4 Emissions,2017,32,85,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,165,154,164,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
1,166,135,164,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
1,167,153,164,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
1,168,169,4,4,0,0,22,0,0,0,-1--1--1,,1|(1400,566)|
11,169,0,1170,566,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,170,C from CH4 oxidation,1170,592,82,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,171,48,1018,566,25,15,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,172,169,171,100,0,0,22,0,0,0,-1--1--1,,1|(1103,566)|
10,173,CH4 PER C,993,614,53,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,174,MATRIX UNIT PREFIXES,1108,686,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,175,173,169,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,176,174,169,1,0,0,0,2,64,0,-1--1--1,|||0-0-0,1|(1181,623)|
10,177,init CO2 in atmosphere ppm,1248,282,105,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,178,177,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,179,pre industrial ppm CO2,2179,786,97,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,180,Temperature change base 1850,2046,499,82,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,181,180,51,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,182,180,73,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,183,Temperature change base 1850,1715,-127,82,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,184,183,139,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,185,CH4 Uptake,957,534,44,15,8,3,0,32,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,186,185,169,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,187,CH4 Fractional Uptake,836,609,81,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,188,187,185,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
10,189,CH4 in Atm,834,534,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,190,189,185,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
10,191,Anthropogenic CO2 Emissions wo LUC,998,256,104,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,192,GtC PER ppm,1283,225,51,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,193,192,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,194,192,7,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,195,Reference Sensitivity of C from Permafrost and Clathrate to Temperature SP,477,650,136,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,196,C in permafrost,400,448,67,23,3,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,197,199,196,100,0,0,22,0,192,0,-1--1--1,,1|(607,426)|
1,198,199,4,4,0,0,22,0,192,0,-1--1--1,,1|(1060,426)|
11,199,0,754,426,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,200,Flux C from permafrost thaw,754,457,85,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,201,195,200,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,202,SWITCH Sensitivity of Methane Emissions to Permafrost and Clathrate,374,499,124,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,203,202,200,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,204,Temperature change base 1850,539,561,77,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,205,204,200,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,206,Temperature Threshold for Methane Emissions from Permafrost and Clathrate SP,211,547,141,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,207,206,200,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,208,Initial C in permafrost,391,367,75,9,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,209,208,196,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
10,210,Anthropogenic LUC CO2 Emissions,1495,265,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,211,210,31,1,0,0,0,0,192,0,-1--1--1,,1|(1517,303)|
10,212,Fossil Reserves,639,183,65,23,3,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,213,Fossil Resources,691,-25,71,23,3,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,214,Coal Reserves,602,95,48,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,215,Gas Reserves,715,81,46,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,216,Oil Reserves,800,102,43,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,217,Coal Resources,488,-49,52,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,218,Oil Resources,429,3,47,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,219,Gas Resources,423,46,50,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,220,214,212,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,221,215,212,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,222,216,212,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,223,217,213,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,224,218,213,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,225,219,213,0,0,0,0,0,192,1,-1--1--1,,1|(0,0)|
1,226,228,212,100,0,0,22,0,192,0,-1--1--1,,1|(639,301)|
1,227,228,4,4,0,0,22,0,192,0,-1--1--1,,1|(1400,301)|
11,228,0,1032,301,8,6,33,3,0,0,1,0,0,0,0,0,0,0,0,0
10,229,Anthropogenic C combustion,1032,330,83,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,230,6,229,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,231,191,229,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
12,232,48,994,-25,25,15,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,233,235,213,100,0,0,22,0,192,0,-1--1--1,,1|(814,-25)|
1,234,235,232,4,0,0,22,0,192,0,-1--1--1,,1|(924,-25)|
11,235,0,873,-25,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,236,Anthropogenic C combustion 0,873,6,88,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,237,191,236,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,238,6,236,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Other GHG Cycle
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,70,0
10,1,CH4 in Atm 0,785,506,52,33,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,2,48,982,502,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,3,4,2,4,0,0,22,0,0,0,-1--1--1,,1|(936,502)|
11,4,0,893,502,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,5,CH4 Uptake 0,893,520,53,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,6,Initial CH4,781,592,40,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,7,ppb CH4 per Mton CH4,720,734,92,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,8,CH4 atm conc,694,639,53,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,9,7,8,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,10,1,8,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,11,7,6,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,12,Initial CH4 conc,814,673,70,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,13,12,6,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,14,CH4 molar mass,803,828,71,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,15,14,7,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,16,MATRIX UNIT PREFIXES,690,838,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,17,16,7,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,18,CH4 Fractional Uptake 0,981,642,93,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,19,Time Const for CH4,1115,603,77,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,20,18,19,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,21,Reference CH4 time constant,1145,686,109,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,22,21,18,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,23,Stratospheric CH4 path share,942,711,111,27,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,24,23,18,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,25,Tropospheric CH4 path share,1062,741,109,27,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,26,25,18,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,27,1,18,1,0,0,0,2,64,0,-1--1--1,|||0-0-0,1|(884,605)|
1,28,4,1,36,0,0,22,2,64,0,-1--1--1,|||0-0-0,1|(861,502)|
1,29,6,1,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,30,Temperature Threshold for Methane Emissions from Permafrost and Clathrate SP,415,656,175,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,31,Reference Sensitivity of CH4 from Permafrost and Clathrate to Temperature SP,240,520,174,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,32,SWITCH Sensitivity of Methane Emissions to Permafrost and Clathrate,271,614,154,27,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,33,Global CH4 emissions,624,333,80,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,34,48,775,351,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,35,37,1,4,0,0,22,0,0,0,-1--1--1,,1|(775,450)|
1,36,37,34,100,0,0,22,0,0,0,-1--1--1,,1|(775,387)|
11,37,0,775,421,8,6,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,38,Global anthropogenic CH4 emissions,880,421,116,27,40,131,0,34,-1,0,0,0,-1--1--1,-1--1--1,Dubai|||0-0-255,0,0,0,0,0,0
12,39,48,519,517,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,40,42,1,4,0,0,22,0,0,0,-1--1--1,,1|(681,528)|
1,41,42,39,100,0,0,22,0,0,0,-1--1--1,,1|(519,528)|
11,42,0,623,528,7,9,34,131,0,0,1,0,0,0,0,0,0,0,0,0
10,43,CH4 Emissions from Permafrost and Clathrate,623,555,131,27,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,44,31,43,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,45,32,43,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,46,30,43,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,47,Total CH4 released,763,924,69,15,0,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,48,50,47,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,49,Total C from permafrost,489,911,89,15,0,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,50,CH4 PER C,593,991,53,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,51,50,49,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,52,CH4 Emissions from Permafrost and Clathrate,595,1133,136,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,53,52,49,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,54,52,47,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
12,55,48,516,478,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,56,58,1,4,0,0,22,0,0,0,-1--1--1,,1|(684,478)|
1,57,58,55,100,0,0,22,0,0,0,-1--1--1,,1|(575,478)|
11,58,0,629,478,6,8,34,3,0,0,3,0,0,0,0,0,0,0,0,0
10,59,Natural CH4 Emissions,629,452,95,13,40,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,60,59,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,61,N2O in Atm,1621,348,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,62,48,1828,349,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,63,64,62,4,0,0,22,0,0,0,-1--1--1,,1|(1781,349)|
11,64,0,1738,349,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,65,N2O Uptake,1738,367,45,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,66,48,1390,348,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,67,68,66,100,0,0,22,0,0,0,-1--1--1,,1|(1437,348)|
11,68,0,1482,348,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,69,Global N2O Emissions,1482,374,82,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,70,Time Const for N2O,1835,433,87,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,71,70,65,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,72,61,64,1,0,0,0,0,64,0,-1--1--1,,1|(1674,285)|
10,73,Initial N2O,1701,457,41,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,74,Natural N2O emissions,1433,457,95,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,75,ppb N2O per MTonN,1581,497,80,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,76,75,77,0,0,0,0,1,64,0,128-128-128,|||0-0-0,1|(0,0)|
10,77,N2O atm conc,1597,429,54,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,78,61,77,0,0,0,0,1,64,0,128-128-128,|||0-0-0,1|(0,0)|
1,79,75,73,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,80,Initial N2O conc,1729,535,71,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,81,80,73,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,82,74,69,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,83,MATRIX UNIT PREFIXES,1386,511,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,84,83,75,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,85,N2O N molar mass,1486,604,83,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,86,85,75,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,87,68,61,4,0,0,22,0,64,0,-1--1--1,,1|(1535,348)|
1,88,64,61,36,0,0,22,2,64,0,-1--1--1,|||0-0-0,1|(1696,349)|
1,89,73,61,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
12,90,0,725,196,65,15,8,7,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai||B|0-0-0,0,0,0,0,0,0
CH4 cycle
12,91,0,1612,197,67,15,8,7,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai||B|0-0-0,0,0,0,0,0,0
N2O cycle
10,92,PFC in Atm,2276,546,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,93,Time Const for PFC,2376,639,84,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,94,Preindustrial PFC,2606,600,63,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,95,ppt PFC per Tons PFC,2463,471,86,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,96,95,97,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,97,PFC atm conc,2305,472,52,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,98,95,94,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,99,Preindustrial PFC conc,2647,334,93,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,100,99,94,1,0,0,0,0,64,1,-1--1--1,,1|(2756,476)|
1,101,92,97,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,102,PFC radiative efficiency,2376,308,94,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,103,PFC RF,2360,377,28,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,104,97,103,1,0,0,0,0,64,0,-1--1--1,,1|(2332,424)|
1,105,102,103,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
12,106,48,2463,547,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,107,108,106,4,0,0,22,0,0,0,-1--1--1,,1|(2418,547)|
11,108,0,2377,547,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,109,PFC uptake,2377,565,41,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,110,92,109,1,0,0,0,0,64,0,-1--1--1,,1|(2306,612)|
1,111,93,109,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,112,Natural PFC emissions,2236,668,83,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,113,48,2035,547,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,114,115,113,100,0,0,22,0,0,0,-1--1--1,,1|(2089,547)|
11,115,0,2140,547,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,116,Global total PFC emissions,2140,573,99,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,117,112,116,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,118,94,112,1,0,0,0,0,64,0,-1--1--1,,1|(2440,737)|
1,119,99,103,1,0,0,0,0,64,0,-1--1--1,,1|(2472,349)|
10,120,CF4 molar mass,2655,480,70,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,121,120,95,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,122,MATRIX UNIT PREFIXES,2504,397,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,123,122,95,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,124,108,92,36,0,0,22,2,64,0,-1--1--1,|||0-0-0,1|(2343,547)|
12,125,0,2335,250,69,15,8,7,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
PFCs cycle
10,126,Init PFC in Atm con,2056,370,87,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,127,115,92,4,0,0,22,0,0,0,-1--1--1,,1|(2191,547)|
10,128,Init PFC in Atm,2178,463,60,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,129,126,128,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,130,95,128,1,0,0,0,0,64,0,-1--1--1,,1|(2326,445)|
1,131,128,92,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
12,132,48,1192,1085,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,133,134,132,100,0,0,22,0,0,0,-1--1--1,,1|(1232,1085)|
11,134,0,1270,1085,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,135,Global SF6 emissions,1270,1111,79,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,136,Time Const for SF6,1552,1233,84,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,137,Preindustrial SF6 conc,1676,847,93,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,138,SF6 RF,1492,909,28,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,139,Initial SF6,1650,1063,38,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,140,SF6 radiative efficiency,1504,849,94,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,141,ppt SF6 per Tons SF6,1635,1000,86,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,142,141,139,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,143,SF6 atm conc,1411,975,52,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,144,141,143,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,145,140,138,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,146,143,138,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,147,137,138,1,0,0,0,0,64,0,-1--1--1,,1|(1621,891)|
10,148,MATRIX UNIT PREFIXES,1813,972,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,149,148,141,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,150,SF6 molar mass,1719,915,70,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,151,150,141,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
12,152,0,1587,757,58,16,8,7,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
SF6 cycle
10,153,Initial SF6 con,1676,1160,65,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,154,153,139,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,155,HFC in Atm,2167,1084,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,156,48,1998,1079,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,157,159,155,4,0,0,22,0,0,0,-1--1--1,,1|(2096,1079)|
1,158,159,156,100,0,0,22,0,0,0,-1--1--1,,1|(2030,1079)|
11,159,0,2059,1079,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,160,Global HFC emissions,2059,1105,80,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,161,Time Const for HFC,2364,1147,85,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,162,Preindustrial HFC conc,2012,881,94,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,163,HFC RF,2151,905,29,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,164,Initial HFC,2299,1041,39,15,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,165,164,155,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,166,HFC radiative efficiency,2278,864,95,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,167,ppt HFC per Tons HFC,2405,969,88,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,168,HFC atm conc,2238,981,53,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,169,155,168,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,170,167,168,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,171,168,163,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
12,172,48,2358,1081,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,173,175,172,4,0,0,22,0,0,0,-1--1--1,,1|(2314,1081)|
1,174,175,155,100,0,0,22,0,0,0,-1--1--1,,1|(2237,1081)|
11,175,0,2274,1081,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,176,HFC uptake,2274,1099,42,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,177,161,176,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,178,155,176,1,0,0,0,0,64,0,-1--1--1,,1|(2192,1137)|
1,179,167,164,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,180,166,163,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,181,HFC molar mass,2437,861,71,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,182,181,167,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,183,162,163,1,0,0,0,0,64,0,-1--1--1,,1|(2125,890)|
12,184,0,2280,771,70,15,8,7,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
HFCs cycle
10,185,Inital HFC con,2574,1122,64,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,186,185,164,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,187,MATRIX UNIT PREFIXES,2560,981,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,188,187,167,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,189,Temperature change base 1850,574,704,82,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,190,189,43,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,191,Preindustrial CH4,1054,542,74,13,8,2,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,192,191,18,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,193,SWITCH RCP POLICY SP,914,236,104,13,8,130,0,34,0,0,0,0,-1--1--1,-1--1--1,Dubai||B|64-160-98,0,0,0,0,0,0
10,194,SWITCH RCP POLICY SP,1410,193,104,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||64-160-98,0,0,0,0,0,0
10,195,SWITCH RCP POLICY SP,2059,765,104,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||64-160-98,0,0,0,0,0,0
10,196,SWITCH RCP POLICY SP,1127,943,104,13,8,130,0,34,-1,0,0,0,-1--1--1,0-0-0,Dubai|||64-160-98,0,0,0,0,0,0
10,197,SWITCH RCP POLICY SP,2050,1008,104,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||64-160-98,0,0,0,0,0,0
10,198,SF6 in Atm,1399,1089,60,21,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,199,134,198,4,0,0,22,0,0,0,-1--1--1,,1|(1308,1085)|
1,200,198,143,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,201,139,198,1,0,0,0,0,128,1,-1--1--1,,1|(1540,1051)|
12,202,48,1592,1088,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,203,205,202,4,0,0,22,0,0,0,-1--1--1,,1|(1554,1088)|
1,204,205,198,100,0,0,22,0,0,0,-1--1--1,,1|(1486,1088)|
11,205,0,1520,1088,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,206,SF6 uptake,1520,1106,41,15,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,207,136,206,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,208,198,206,1,0,0,0,0,128,0,-1--1--1,,1|(1463,1162)|
1,209,18,5,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,210,1,5,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,211,ppt PER ppb,2061,958,57,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,212,211,163,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,213,ppt PER MOL,554,788,62,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,214,213,7,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,215,ppt PER ppb,941,801,57,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,216,215,7,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,217,ppt PER MOL,1650,571,62,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,218,217,75,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,219,ppt PER ppb,1616,653,57,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,220,219,75,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,221,ppt PER ppb,2210,330,57,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,222,221,103,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,223,ppt PER MOL,2644,412,62,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,224,223,95,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,225,ppt PER MOL,2452,1035,62,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,226,225,167,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,227,ppt PER MOL,1798,1046,62,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,228,227,141,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,229,ppt PER ppb,1366,885,57,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,230,229,138,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,231,16,49,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,232,16,47,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,233,38,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,234,Anthropogenic CH4 Emissions,1007,351,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,235,234,38,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,236,Anthropogenic N2O Emissions,1578,254,87,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,237,236,69,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,238,Anthropogenic PFC Emissions,1968,646,86,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,239,238,116,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,240,Anthropogenic SF6 Emissions,1215,1182,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,241,240,135,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,242,Flux C from permafrost thaw,320,879,90,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,243,242,49,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,244,Greenhouse gas emissions,1578,292,85,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,245,244,236,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,246,Greenhouse gas emissions,1968,684,85,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,247,246,238,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,248,93,112,1,0,0,0,0,128,0,-1--1--1,,1|(2354,665)|
10,249,Anthropogenic HFC Emissions,2017,1173,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,250,249,160,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Radiative Forcing
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,70,0
10,1,CH4 and N2O Radiative Forcing,278,274,116,27,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,2,CO2 Radiative Forcing,621,102,82,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,3,RF from F gases,303,424,63,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,4,Halocarbon RF,285,336,52,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,5,3,4,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,6,Preindustrial C,278,141,64,13,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,7,6,2,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
10,8,HFC RF,90,486,38,15,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,9,PFC RF,104,403,37,15,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,10,9,3,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,11,SF6 RF,90,446,37,15,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,12,11,3,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,13,"Well-Mixed GHG Forcing",655,331,91,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,14,2,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,15,1,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,16,4,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,17,Time,1069,388,27,15,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,18,HFC RF total,302,494,49,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,19,18,3,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,20,8,18,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,21,C in Atmosphere,267,73,72,13,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,22,Total Radiative Forcing,866,559,84,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,23,Other Forcings,762,678,54,15,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,24,23,22,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,25,13,22,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,26,Time to Commit RF,1082,589,84,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,27,21,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,28,CH4 reference conc,2037,376,82,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,29,CH4 radiative efficiency coefficient,2010,289,118,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,30,N2O radiative efficiency coefficient,1523,325,119,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,31,N2O reference conc,1534,387,83,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,32,Adjustment for CH4ref and N2O,1577,504,111,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,33,Adjustment for CH4ref and N2Oref,1791,222,116,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,34,Adjustment for CH4 and N2Oref,1946,498,112,27,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,35,N2O reference conc,1424,160,83,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,36,35,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,37,CH4 N2O unit adj,1786,495,79,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,38,CH4 N2O interaction coeffient,1521,107,110,27,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,39,CH4 N2O inter coef 2,1677,99,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,40,CH4 N2O inter coef 3,1814,95,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,41,CH4 N20 inter exp,1945,103,82,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,42,CH4 N20 inter exp 2,2062,114,92,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,43,39,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,44,38,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,45,42,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,46,41,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,47,40,33,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,48,CH4 N2O interaction coeffient,1326,396,110,27,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,49,CH4 N2O inter coef 2,1318,443,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,50,CH4 N2O inter coef 3,1318,496,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,51,CH4 N20 inter exp,1318,549,82,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,52,CH4 N20 inter exp 2,1318,605,92,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,53,49,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,54,48,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,55,52,32,1,0,0,0,0,64,0,-1--1--1,,1|(1452,583)|
1,56,50,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,57,51,32,1,0,0,0,0,64,0,-1--1--1,,1|(1429,555)|
10,58,CH4 N2O unit adj,1339,275,79,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,59,58,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,60,CH4 reference conc,1334,343,82,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,61,60,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,62,N2O atm conc,1703,578,65,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,63,CH4 atm conc,1900,579,64,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,64,62,32,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,65,63,34,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,66,N2O Radiative Forcing,1713,417,83,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,67,32,66,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,68,33,66,1,0,0,0,0,64,0,-1--1--1,,1|(1680,303)|
1,69,62,66,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,70,31,66,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,71,30,66,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,72,37,66,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,73,CH4 Radiative Forcing,1875,412,82,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,74,34,73,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,75,33,73,1,0,0,0,0,64,0,-1--1--1,,1|(1855,297)|
1,76,63,73,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,77,28,73,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,78,29,73,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,79,37,73,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,80,CH4 N2O interaction coeffient,2230,396,110,27,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,81,CH4 N2O inter coef 2,2224,443,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,82,CH4 N2O inter coef 3,2224,496,95,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,83,CH4 N20 inter exp,2224,549,82,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,84,CH4 N20 inter exp 2,2224,605,92,13,8,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,85,CH4 N2O unit adj,2224,269,79,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,86,85,34,1,0,0,0,0,128,0,-1--1--1,,1|(2099,391)|
1,87,80,34,1,0,0,0,0,128,0,-1--1--1,,1|(2138,456)|
1,88,81,34,1,0,0,0,0,128,0,-1--1--1,,1|(2135,477)|
1,89,83,34,1,0,0,0,0,128,0,-1--1--1,,1|(2127,537)|
1,90,84,34,1,0,0,0,0,128,0,-1--1--1,,1|(2115,578)|
1,91,82,34,1,0,0,0,0,128,0,-1--1--1,,1|(2131,506)|
10,92,CH4 reference conc,2183,158,82,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,93,92,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,94,58,33,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,95,N2O reference conc,2224,337,83,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,96,95,34,1,0,0,0,0,128,0,-1--1--1,,1|(2099,427)|
10,97,CH4 and N2O Radiative Forcing,1783,338,111,27,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,98,66,97,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,99,73,97,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,100,"Other GHG Rad Forcing (non CO2)",903,284,114,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,101,2,100,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,102,22,100,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,103,Effective Radiative Forcing,1006,483,96,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,104,26,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,105,17,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,106,22,103,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,107,CO2 Rad Force coefficient,267,204,106,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,108,107,2,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,109,CO2e ppm concentrations,472,238,94,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,110,13,109,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,111,pre industrial ppm CO2,567,190,97,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,112,111,109,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,113,107,109,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,114,Time,762,715,26,11,8,2,1,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,115,Ozone,977,828,22,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,116,Stratospheric water vapour,540,681,80,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,117,Aerosol radiation interactions,712,809,84,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,118,Aerosol cloud interactions,550,774,80,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,119,Land use,852,847,32,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,120,Surface albedo,988,761,50,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,121,Contrails and aviation induced cirrus,1072,688,94,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,122,116,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,123,118,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,124,117,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,125,119,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,126,115,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,127,120,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,128,121,23,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,129,Other halocarbon,106,299,57,11,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,130,129,4,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Total GHG Emissions
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,84,0
10,1,Global HFC emissions,1453,187,89,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,2,Global SF6 emissions,1454,259,88,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,3,GWP 100 year,1475,658,66,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,4,GWP 20 year,1473,584,60,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,5,MATRIX UNIT PREFIXES,1472,732,100,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,6,SWITCH GWP TIME FRAME SP,1463,517,116,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,7,Other GHG emissions,1867,361,80,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,8,1,7,1,0,0,0,0,128,0,-1--1--1,,1|(1660,237)|
1,9,2,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,10,6,7,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,11,4,7,1,0,0,0,0,128,0,-1--1--1,,1|(1707,472)|
1,12,3,7,1,0,0,0,0,128,0,-1--1--1,,1|(1698,528)|
1,13,5,7,1,0,0,0,0,128,0,-1--1--1,,1|(1730,564)|
10,14,Cumulative GHG emissions GtCe,777,194,110,27,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,15,C PER CO2,895,87,53,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,16,15,14,0,0,0,0,0,0,0,-1--1--1,,1|(0,0)|
12,17,48,1188,299,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,18,20,22,4,0,0,22,0,0,0,-1--1--1,,1|(998,299)|
1,19,20,17,100,0,0,22,0,0,0,-1--1--1,,1|(1128,299)|
11,20,0,1072,299,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,21,Total GHG emissions GtCO2e wo LUC,1072,325,109,13,40,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,22,Cumulative GHG emissions GtCO2e,855,302,76,24,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,23,22,14,1,0,0,0,0,128,0,-1--1--1,,1|(808,257)|
10,24,Total cumulative CO2 emissions GtCO2,853,558,92,28,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,25,Total cumulative C emissions GtC,1025,696,112,27,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,26,24,25,1,0,0,0,0,64,0,-1--1--1,,1|(946,582)|
10,27,Initial cumulative CO2 emissions,913,474,116,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,28,27,24,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,29,C PER CO2,833,739,53,15,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,30,29,25,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,31,1,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,32,2,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,33,6,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,34,4,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,35,3,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,36,5,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,37,Global anthropogenic CH4 emissions,1450,117,120,27,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,38,37,21,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,39,37,7,1,0,0,0,0,128,0,-1--1--1,,1|(1729,187)|
10,40,Anthropogenic CO2 Emissions wo LUC,810,679,104,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,41,40,24,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,42,Anthropogenic CO2 Emissions wo LUC,1206,122,104,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,43,42,21,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,44,Anthropogenic N2O Emissions,1421,433,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,45,44,7,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,46,44,21,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,47,Anthropogenic PFC Emissions,1415,361,91,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,48,47,21,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
1,49,47,7,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,50,Anthropogenic LUC CO2 Emissions,632,597,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,51,50,24,0,0,0,0,0,192,0,-1--1--1,,1|(0,0)|
10,52,Global anthropogenic CH4 emissions in CO2equivalents,777,-276,117,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,53,GWP 100 year,1182,-86,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,54,53,52,1,0,0,0,0,64,0,-1--1--1,,1|(961,-127)|
10,55,GWP 20 year,1179,-154,58,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,56,55,52,1,0,0,0,0,64,0,-1--1--1,,1|(993,-170)|
10,57,MATRIX UNIT PREFIXES,1178,-231,86,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,58,57,52,1,0,0,0,0,64,0,-1--1--1,,1|(1011,-236)|
10,59,SWITCH GWP TIME FRAME SP,1184,-316,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,60,59,52,1,0,0,0,0,64,0,-1--1--1,,1|(968,-313)|
10,61,Global anthropogenic CH4 emissions,1186,-397,120,27,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,62,61,52,1,0,0,0,0,128,0,-1--1--1,,1|(947,-371)|
10,63,Global anthropogenic N2O emissions in CO2equivalents,1429,-283,114,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,64,Anthropogenic N2O Emissions,1822,-181,89,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,65,64,63,1,0,0,0,0,64,0,-1--1--1,,1|(1632,-221)|
10,66,GWP 100 year,1813,-119,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,67,66,63,1,0,0,0,0,64,0,-1--1--1,,1|(1624,-161)|
10,68,GWP 20 year,1824,-248,58,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,69,68,63,1,0,0,0,0,64,0,-1--1--1,,1|(1651,-252)|
10,70,MATRIX UNIT PREFIXES,1820,-318,86,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,71,70,63,1,0,0,0,0,64,0,-1--1--1,,1|(1627,-314)|
10,72,SWITCH GWP TIME FRAME SP,1823,-395,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,73,72,63,1,0,0,0,0,64,0,-1--1--1,,1|(1623,-369)|
10,74,Global anthropogenic HFC emissions in CO2equivalents,2229,-270,118,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,75,Global anthropogenic PFC emissions in CO2equivalents,2200,203,117,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,76,Anthropogenic PFC Emissions,2579,199,91,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,77,76,75,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,78,GWP 100 year,2606,360,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,79,78,75,1,0,0,0,0,64,0,-1--1--1,,1|(2414,336)|
10,80,GWP 20 year,2598,287,58,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,81,80,75,1,0,0,0,0,64,0,-1--1--1,,1|(2424,264)|
10,82,MATRIX UNIT PREFIXES,2586,113,86,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,83,82,75,1,0,0,0,0,64,0,-1--1--1,,1|(2387,145)|
10,84,SWITCH GWP TIME FRAME SP,2602,28,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,85,84,75,1,0,0,0,0,64,0,-1--1--1,,1|(2378,86)|
10,86,Global anthropogenic SF6 emissions in CO2equivalents,2190,562,115,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,87,Global SF6 emissions,2586,700,83,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,88,87,86,1,0,0,0,0,64,0,-1--1--1,,1|(2388,668)|
10,89,GWP 100 year,2591,622,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,90,89,86,1,0,0,0,0,64,0,-1--1--1,,1|(2420,619)|
10,91,GWP 20 year,2594,562,58,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,92,91,86,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,93,MATRIX UNIT PREFIXES,2599,494,86,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,94,93,86,1,0,0,0,0,64,0,-1--1--1,,1|(2409,505)|
10,95,SWITCH GWP TIME FRAME SP,2610,432,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,96,95,86,1,0,0,0,0,64,0,-1--1--1,,1|(2382,466)|
10,97,Global HFC emissions,2625,-265,56,20,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,98,97,74,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,99,GWP 100 year,2626,-143,63,9,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,100,99,74,1,0,0,0,0,64,0,-1--1--1,,1|(2436,-178)|
10,101,GWP 20 year,2626,-204,58,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,102,101,74,1,0,0,0,0,64,0,-1--1--1,,1|(2461,-213)|
10,103,MATRIX UNIT PREFIXES,2626,-328,86,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,104,103,74,1,0,0,0,0,64,0,-1--1--1,,1|(2444,-314)|
10,105,SWITCH GWP TIME FRAME SP,2627,-393,97,19,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,106,105,74,1,0,0,0,0,64,0,-1--1--1,,1|(2394,-357)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Temperature Change
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,75,0
10,1,Atm and Upper Ocean Heat Cap,1366,317,109,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,2,global surface area,1286,252,79,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,3,2,1,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,4,volumetric heat capacity,1521,337,89,13,8,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,5,4,1,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,6,upper layer volume Vu,1501,268,84,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,7,6,1,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,8,WATER DENSITY,1532,434,75,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,9,8,4,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,10,SPECIFIC HEAT CAPACITY WATER,1636,528,121,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,11,10,4,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,12,sec per yr,1633,377,39,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,13,12,4,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,14,WATT PER J s,1645,318,68,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,15,14,4,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,16,2,6,1,0,0,0,0,64,1,-1--1--1,,1|(1348,206)|
10,17,land area fraction,1711,281,74,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,18,17,6,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,19,land thickness,1600,189,60,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,20,19,6,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
12,21,0,1489,108,172,47,8,7,0,36,-1,0,0,0,0-0-0,192-192-192,Dubai|||255-0-255,0,0,0,0,0,0
Illustrative calculation of surface land/ocean heat capacity, as in S. Schneider & S. Thompson (1981) "Atmospheric CO2 and Climate: Importance of the Transient Response" Journal of Geophysical Research, Vol. 86 No. C4 Pgs. 3135-314
10,22,Deep Ocean Heat Cap,1402,399,82,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,23,lower layer volume Vu,1309,462,83,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,24,23,22,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,25,30,23,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,26,4,22,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,27,2,23,1,0,0,0,0,64,1,-1--1--1,,1|(1231,343)|
1,28,17,23,1,0,0,0,0,64,1,-1--1--1,,1|(1675,389)|
1,29,2,22,1,0,0,0,0,64,1,-1--1--1,,1|(1285,337)|
10,30,Layer Depth,1466,472,53,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,31,Climate Feedback Param,734,190,86,15,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,32,Relative Deep Ocean Temp,433,571,98,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,33,31,47,1,0,0,0,0,0,0,-1--1--1,,1|(699,224)|
10,34,Heat in Atmosphere and Upper Ocean,595,362,55,27,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,35,Heat in Deep Ocean,594,555,56,27,3,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,36,38,35,4,0,0,22,0,0,0,-1--1--1,,1|(593,490)|
1,37,38,34,100,0,0,22,0,0,0,-1--1--1,,1|(593,414)|
11,38,0,593,446,8,7,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,39,Heat Transfer,676,446,50,15,32,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,40,48,853,362,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,41,49,34,4,0,0,22,0,0,0,-1--1--1,,1|(703,362)|
1,42,49,40,100,0,0,22,0,0,0,-1--1--1,,1|(807,362)|
12,43,48,593,175,10,8,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,44,46,43,4,0,0,22,0,0,0,-1--1--1,,1|(593,212)|
1,45,46,34,100,0,0,22,0,0,0,-1--1--1,,1|(593,295)|
11,46,0,593,248,8,7,33,3,0,0,4,0,0,0,0,0,0,0,0,0
10,47,Feedback Cooling,676,248,61,15,32,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,48,35,32,1,0,0,0,0,64,0,-1--1--1,,1|(524,606)|
11,49,0,764,362,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,50,Effective Radiative Forcing,764,400,103,15,32,2,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,51,Deep Ocean Heat Cap,629,659,91,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,52,Heat Transfer Coeff,823,468,73,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,53,52,39,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,54,Mean Depth of Adjacent Layers,766,552,115,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,55,54,39,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,56,32,38,1,0,0,0,0,64,0,-1--1--1,,1|(512,494)|
1,57,54,52,1,0,0,0,0,64,1,-1--1--1,,1|(809,513)|
10,58,Heat Diffusion Covar,996,534,86,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,59,58,52,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,60,Heat Transfer Rate,917,592,80,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,61,60,52,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,62,SECONDS PER YEAR,1699,472,90,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,63,62,12,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,64,Atm and Upper Ocean Heat Cap,446,280,114,27,8,130,0,34,-1,0,0,0,0-0-0,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,65,64,34,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,66,51,35,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
1,67,51,32,1,0,0,0,0,64,0,-1--1--1,,1|(491,647)|
10,68,Mixed Depth,1444,179,55,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,69,68,6,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,70,init Atmos UOcean Temp,764,307,104,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,71,70,34,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,72,Init Deep Ocean Temp,767,615,93,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,73,72,35,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,74,"2x CO2 Forcing",801,125,58,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,75,74,31,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,76,DAYS PER YEAR,1788,422,74,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,77,76,12,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,78,CO2 Rad Force coefficient,836,66,106,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,79,78,74,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,80,Eddy diff coeff index,1016,344,87,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,81,Eddy diff coeff 0,1011,407,65,13,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,82,Eddy diff mean,1014,472,66,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,83,82,81,0,0,0,0,0,0,1,-1--1--1,,1|(0,0)|
1,84,80,81,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,85,81,52,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
1,86,82,52,0,0,0,0,0,128,1,-1--1--1,,1|(0,0)|
10,87,Equilibrium climate sensitivity SP,598,74,109,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,88,87,31,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,89,Temperature change base 1750,151,457,86,19,8,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,90,Temperature change base 1850,303,383,71,25,8,131,0,0,-1,0,0,0,0,0,0,0,0,0
10,91,Year threshold of 2°C exceeded,1522,630,73,31,3,131,0,0,0,0,0,0,0,0,0,0,0,0
1,92,34,90,1,0,0,0,0,0,0,-1--1--1,,1|(487,375)|
1,93,64,90,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,94,90,89,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,95,90,46,1,0,0,0,0,128,0,-1--1--1,,1|(336,235)|
1,96,90,38,1,0,0,0,0,128,0,-1--1--1,,1|(461,434)|
12,97,48,1211,627,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,98,100,91,4,0,0,22,0,0,0,-1--1--1,,1|(1395,627)|
1,99,100,97,100,0,0,22,0,0,0,-1--1--1,,1|(1275,627)|
11,100,0,1335,627,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,101,Flow threshold of 2°C exceeded,1335,654,89,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,102,Year threshold of 3°C exceeded,1527,748,73,34,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,103,48,1213,746,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,104,106,102,4,0,0,22,0,0,0,-1--1--1,,1|(1399,746)|
1,105,106,103,100,0,0,22,0,0,0,-1--1--1,,1|(1277,746)|
11,106,0,1338,746,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,107,Flow threshold of 3°C exceeded,1338,773,89,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,108,Year threshold of 4°C exceeded,1533,862,73,34,3,131,0,0,0,0,0,0,0,0,0,0,0,0
12,109,48,1219,860,10,8,0,3,0,0,-1,0,0,0,0,0,0,0,0,0
1,110,112,108,4,0,0,22,0,0,0,-1--1--1,,1|(1405,860)|
1,111,112,109,100,0,0,22,0,0,0,-1--1--1,,1|(1283,860)|
11,112,0,1344,860,6,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,113,Flow threshold of 4°C exceeded,1344,887,89,19,40,3,0,0,-1,0,0,0,0,0,0,0,0,0
10,114,Threshold of 2°C exceeded,1760,630,82,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,115,Threshold of 3°C exceeded,1765,749,82,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
10,116,Threshold of 4°C exceeded,1770,864,82,19,8,3,0,0,0,0,0,0,0,0,0,0,0,0
1,117,91,114,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,118,102,115,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,119,108,116,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,120,Temperature change base 1850,1062,747,69,25,8,130,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,121,120,101,1,0,0,0,0,128,0,-1--1--1,,1|(1172,689)|
1,122,120,107,1,0,0,0,0,128,0,-1--1--1,,1|(1200,772)|
1,123,120,112,1,0,0,0,0,128,0,-1--1--1,,1|(1222,822)|
1,124,91,101,1,0,0,0,0,128,0,-1--1--1,,1|(1442,678)|
10,125,Time,1396,706,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,126,125,101,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,127,TIME STEP,1260,706,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,128,127,101,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,129,127,106,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,130,125,106,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
10,131,Time,1416,941,26,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
10,132,TIME STEP,1280,941,52,11,8,2,0,3,-1,0,0,0,128-128-128,0-0-0,|||128-128-128,0,0,0,0,0,0
1,133,132,113,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,134,131,113,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
1,135,102,107,1,0,0,0,0,128,0,-1--1--1,,1|(1445,797)|
1,136,108,113,1,0,0,0,0,64,0,-1--1--1,,1|(1456,905)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*pH Ocean
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,100,0
10,1,pH in 2000,416,87,45,15,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,2,pH ocean,548,197,35,15,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,3,2,1,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,4,Time,397,-55,27,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,5,4,1,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,6,Delta pH from 2000,223,181,78,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,7,2,6,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,8,1,6,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,9,Time,97,263,27,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,10,9,6,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,11,pH constant 1,479,377,64,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,12,11,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,13,pH constant 2,630,332,64,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,14,13,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,15,pH constant 3,718,267,64,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,16,15,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,17,pH constant 4,795,180,64,13,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,18,17,2,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,19,atmospheric concentrations CO2,662,18,112,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,20,19,2,1,0,0,0,0,128,0,-1--1--1,,1|(576,97)|
10,21,Aragonite saturation,255,368,74,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,22,2,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
12,23,0,443,-148,48,15,8,7,0,40,-1,0,0,0,-1--1--1,0-0-0,Dubai|18||0-0-0,0,0,0,0,0,0
pH ocean
10,24,Oceanic pH threshold,817,472,79,13,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,25,11,24,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,26,13,24,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,27,15,24,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,28,17,24,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,29,ARAGONITE SATURATION CORRECTION FACTOR,177,460,120,26,8,131,0,0,0,0,0,0,0,0,0,0,0,0
1,30,29,21,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
\\\---/// Sketch information - do not modify anything except names
V300  Do not put anything below this section - it will be ignored
*Sea level rise
$192-192-192,0,Times New Roman|12||0-0-0|0-0-0|0-0-255|-1--1--1|255-255-255|96,96,82,0
10,1,Sea Level Rise,890,213,40,20,3,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
12,2,48,710,208,25,15,0,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,3,5,1,4,0,0,22,0,0,0,-1--1--1,,1|(821,208)|
1,4,5,2,100,0,0,22,0,0,0,-1--1--1,,1|(756,208)|
11,5,0,785,208,7,8,34,3,0,0,1,0,0,0,0,0,0,0,0,0
10,6,Change in Sea Level,785,234,75,13,40,3,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,7,Sensitivity of Sea Level Rise to Temperature,244,92,132,27,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,8,7,9,1,0,0,0,0,64,0,-1--1--1,,1|(309,108)|
10,9,Adjusted Sensitivity of Sea Level Rise to Temperature,437,183,141,27,8,131,0,34,0,0,0,0,-1--1--1,-1--1--1,Dubai|||0-0-255,0,0,0,0,0,0
10,10,initial sea level rise in 2019,969,293,107,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,11,Change in Relative Temperature,666,392,109,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,12,Sensitivity of SLR rate to temp rate,838,411,123,27,8,130,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,13,Equilibrium Change in Sea Level,625,260,109,27,8,131,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
10,14,Reference Temperature,682,138,91,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,15,14,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,16,13,6,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,17,9,13,1,0,0,0,0,64,0,-1--1--1,,1|(494,220)|
1,18,10,1,0,0,0,0,0,64,1,-1--1--1,,1|(0,0)|
10,19,TIME STEP,604,465,51,15,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,20,19,11,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,21,Temp Adjustment for SLR,457,437,106,13,8,130,0,35,0,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
10,22,Instant Change in Sea Level,732,318,104,13,8,3,0,32,0,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,23,11,22,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,24,12,22,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,25,22,6,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,26,Adjusted Temperature change from preindustrial for SLR estimation,354,314,158,27,8,131,0,32,-1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
1,27,26,13,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,28,21,26,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
1,29,26,11,0,0,0,0,0,64,0,-1--1--1,,1|(0,0)|
10,30,Temperature change base 1850,254,438,82,13,8,2,0,35,-1,0,0,0,128-128-128,0-0-0,Dubai|||128-128-128,0,0,0,0,0,0
1,31,30,26,0,0,0,0,0,128,0,-1--1--1,,1|(0,0)|
12,32,0,1557,270,355,293,3,188,0,32,1,0,0,0,0-0-0,0-0-0,Dubai|||0-0-0,0,0,0,0,0,0
Sea_level_rise
\\\---/// Sketch information - do not modify anything except names
