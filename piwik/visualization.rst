ViewDataTable
$view = Piwik\ViewDataTable\Factory::build(
$type,
$apiAction,
$controllerMethod
);
$view->config->show_limit_control = false;

table
tableAllColumns
tableGoals
graphVerticalBar
graphPie
graphEvolution
cloud
sparkline


Visualization isa ViewDataTable

Plugin\Visualization($controller, $apiMethod, $params)

    const ID = 'simpleTable';
    const TEMPLATE_FILE     = '@ExampleVisualization/simpleTable.twig';
    const FOOTER_ICON_TITLE = 'Simple Table';
    const FOOTER_ICON       = 'plugins/ExampleVisualization/images/table.png';

[-] Locals
 |-[-] $view(Piwik\Plugins\CoreVisualizations\Visualizations\JqplotGraph\Evolution)
 |  |-     selectableRows[0]                
 |  |-     *Piwik\Plugin\Visualization*templateVars[0] 
 |  |-     *Piwik\Plugin\Visualization*reportLastUpdatedMessage null
 |  |-     *Piwik\Plugin\Visualization*metadata null
 |  |-[+] metricsFormatter(Piwik\Metrics\Formatter\Html)
 |  |-[-] report(Piwik\Plugins\MobileAnalytics\Reports\GetNewDevice)
 |  |  |-[+] orderOfReports[12]               
 |  |  |-     module                           MobileAnalytics
 |  |  |-     action                           getNewDevice
 |  |  |-     name                             NewDevice
 |  |  |-     documentation                    New device installed the application
 |  |  |-     category                         General_Visitors
 |  |  |-     widgetTitle                      null
 |  |  |-     widgetParams[0]                  
 |  |  |-     menuTitle                        MobileAnalytics_NewDevice
 |  |  |-[+] metrics[4]                       
 |  |  |-[+] processedMetrics[4]              
 |  |  |-     hasGoalMetrics                   false
 |  |  |-     constantRowsCount                false
 |  |  |-     isSubtableReport                 false
 |  |  |-     parameters                       null
 |  |  |-     dimension                        null
 |  |  |-     actionToLoadSubTables            
 |  |  |-     order                            1
 |  |  |-     recursiveLabelSeparator           - 
 |  |  |-     defaultSortColumn                nb_visits
 |  |  ‘-     defaultSortOrderDesc             true
 |  |-     dataTable                        null
 |  |-[-] config(Piwik\Plugins\CoreVisualizations\Visualizations\JqplotGraph\Evolution\Config)
 |  |  |-     show_line_graph                  true
 |  |  |-     external_series_toggle           false
 |  |  |-     external_series_toggle_show_all  false
 |  |  |-     x_axis_step_size                 false
 |  |  |-     allow_multi_select_series_picker true
 |  |  |-     max_graph_elements               false
 |  |  |-     selectable_columns               false
 |  |  |-     row_picker_match_rows_by         false
 |  |  |-     rows_to_display                  false
 |  |  |-     selectable_rows                  selectable_rows
 |  |  |-     show_all_ticks                   false
 |  |  |-     add_total_row                    false
 |  |  |-     show_series_picker               true
 |  |  |-     display_percentage_in_tooltip    true
 |  |  |-[-] clientSideProperties[12]         
 |  |  |  |-     0                                show_limit_control
 |  |  |  |-     1                                pivot_by_dimension
 |  |  |  |-     2                                pivot_by_column
 |  |  |  |-     3                                pivot_dimension_name
 |  |  |  |-     4                                show_series_picker
 |  |  |  |-     5                                allow_multi_select_series_picker
 |  |  |  |-     6                                selectable_columns
 |  |  |  |-     7                                selectable_rows
 |  |  |  |-     8                                display_percentage_in_tooltip
 |  |  |  |-     9                                external_series_toggle
 |  |  |  |-     10                               external_series_toggle_show_all
 |  |  |  ‘-     11                               show_line_graph
 |  |  |-[-] overridableProperties[30]        
 |  |  |  |-     0                                show_goals
 |  |  |  |-     1                                show_exclude_low_population
 |  |  |  |-     2                                show_flatten_table
 |  |  |  |-     3                                show_pivot_by_subtable
 |  |  |  |-     4                                show_table
 |  |  |  |-     5                                show_table_all_columns
 |  |  |  |-     6                                show_footer
 |  |  |  |-     7                                show_footer_icons
 |  |  |  |-     8                                show_all_views_icons
 |  |  |  |-     9                                show_active_view_icon
 |  |  |  |-     10                               show_related_reports
 |  |  |  |-     11                               show_limit_control
 |  |  |  |-     12                               show_search
 |  |  |  |-     13                               enable_sort
 |  |  |  |-     14                               show_bar_chart
 |  |  |  |-     15                               show_pie_chart
 |  |  |  |-     16                               show_tag_cloud
 |  |  |  |-     17                               show_export_as_rss_feed
 |  |  |  |-     18                               show_ecommerce
 |  |  |  |-     19                               search_recursive
 |  |  |  |-     20                               show_export_as_image_icon
 |  |  |  |-     21                               show_pagination_control
 |  |  |  |-     22                               show_offset_information
 |  |  |  |-     23                               hide_annotations_view
 |  |  |  |-     24                               export_limit
 |  |  |  |-     25                               columns_to_display
 |  |  |  |-     26                               show_all_ticks
 |  |  |  |-     27                               show_series_picker
 |  |  |  |-     28                               x_axis_step_size
 |  |  |  ‘-     29                               show_line_graph
 |  |  |-     footer_icons                     false
 |  |  |-     show_visualization_only          false
 |  |  |-     show_goals                       false
 |  |  |-     show_insights                    true
 |  |  |-[-] translations[8]                  
 |  |  |  |-     nb_visits                        Visits
 |  |  |  |-     nb_uniq_visitors                 Unique visitors
 |  |  |  |-     nb_actions                       Actions
 |  |  |  |-     nb_users                         Users
 |  |  |  |-     nb_actions_per_visit             Actions per Visit
 |  |  |  |-     avg_time_on_site                 Avg. Time on Website
 |  |  |  |-     bounce_rate                      Bounce Rate
 |  |  |  ‘-     conversion_rate                  Conversion Rate
 |  |  |-     show_exclude_low_population      false
 |  |  |-     show_flatten_table               true
 |  |  |-     show_pivot_by_subtable           false
 |  |  |-     pivot_by_dimension               false
 |  |  |-     pivot_by_column                  
 |  |  |-     pivot_dimension_name             false
 |  |  |-     show_table                       false
 |  |  |-     show_table_all_columns           false
 |  |  |-     show_footer                      true
 |  |  |-     show_footer_icons                true
 |  |  |-[-] columns_to_display[5]            
 |  |  |  |-     0                                label
 |  |  |  |-     1                                nb_visits
 |  |  |  |-     2                                nb_uniq_visitors
 |  |  |  |-     3                                nb_actions
 |  |  |  ‘-     4                                nb_users
 |  |  |-     show_all_views_icons             false
 |  |  |-     show_active_view_icon            true
 |  |  |-     related_reports[0]               
 |  |  |-     related_reports_title            Related reports:
 |  |  |-     title                            
 |  |  |-     show_related_reports             true
 |  |  |-     documentation                    false
 |  |  |-[-] custom_parameters[1]             
 |  |  |  ‘-     viewDataTable                    graphEvolution
 |  |  |-     show_limit_control               false
 |  |  |-     show_search                      false
 |  |  |-     enable_sort                      true
 |  |  |-     show_bar_chart                   true
 |  |  |-     show_pie_chart                   true
 |  |  |-     show_tag_cloud                   true
 |  |  |-     show_export_as_rss_feed          true
 |  |  |-     show_ecommerce                   false
 |  |  |-     show_footer_message              false
 |  |  |-     metrics_documentation[0]         
 |  |  |-     tooltip_metadata_name            false
 |  |  |-     self_url                         ?date=2016-03-09&module=MobileAnalytics&action=newDevice&widget=1&idSite=3&period=day
 |  |  |-     datatable_css_class              false
 |  |  |-     datatable_js_type                DataTable
 |  |  |-     search_recursive                 false
 |  |  |-     y_axis_unit                      
 |  |  |-     show_export_as_image_icon        true
 |  |  |-     filters[0]                       
 |  |  |-     subtable_controller_action       newDevice
 |  |  |-     show_pagination_control          false
 |  |  |-     show_offset_information          false
 |  |  |-     hide_annotations_view            false
 |  |  |-     export_limit                     100
 |  |  |-     report_id                        MobileAnalytics.newDevice
 |  |  |-     controllerName                   MobileAnalytics
 |  |  ‘-     controllerAction                 newDevice
 |  |-[-] requestConfig(Piwik\ViewDataTable\RequestConfig)
 |  |  |-[-] clientSideParameters[11]         
 |  |  |  |-     0                                filter_excludelowpop
 |  |  |  |-     1                                filter_excludelowpop_value
 |  |  |  |-     2                                filter_pattern
 |  |  |  |-     3                                filter_column
 |  |  |  |-     4                                filter_offset
 |  |  |  |-     5                                flat
 |  |  |  |-     6                                expanded
 |  |  |  |-     7                                pivotBy
 |  |  |  |-     8                                pivotByColumn
 |  |  |  |-     9                                pivotByColumnLimit
 |  |  |  ‘-     10                               columns
 |  |  |-[-] overridableProperties[15]        
 |  |  |  |-     0                                filter_sort_column
 |  |  |  |-     1                                filter_sort_order
 |  |  |  |-     2                                filter_limit
 |  |  |  |-     3                                filter_offset
 |  |  |  |-     4                                filter_pattern
 |  |  |  |-     5                                filter_column
 |  |  |  |-     6                                filter_excludelowpop
 |  |  |  |-     7                                filter_excludelowpop_value
 |  |  |  |-     8                                disable_generic_filters
 |  |  |  |-     9                                disable_queued_filters
 |  |  |  |-     10                               flat
 |  |  |  |-     11                               expanded
 |  |  |  |-     12                               pivotBy
 |  |  |  |-     13                               pivotByColumn
 |  |  |  ‘-     14                               pivotByColumnLimit
 |  |  |-     filter_sort_column               false
 |  |  |-     filter_sort_order                desc
 |  |  |-     filter_limit                     false
 |  |  |-     flat                             false
 |  |  |-     expanded                         false
 |  |  |-     filter_offset                    0
 |  |  |-     filter_pattern                   false
 |  |  |-     filter_column                    false
 |  |  |-     filter_excludelowpop             false
 |  |  |-     filter_excludelowpop_value       false
 |  |  |-     request_parameters_to_modify[0]  
 |  |  |-     disable_generic_filters          false
 |  |  |-     disable_queued_filters           false
 |  |  |-     apiMethodToRequestDataTable      MobileAnalytics.getNewDevice
 |  |  |-     idSubtable                       0
 |  |  |-     pivotBy                          false
 |  |  |-     pivotByColumn                    false
 |  |  ‘-     pivotByColumnLimit               false
