Archive::build($idSites, $period, $strDate, $segment)
period: day, week, month, year, range
date: YYYY-MM-DD, today, range

getNumeric($names)
返回某个指标数据

get($names, 'numeric')
getPluginForReport($metric_name):
在 Metrics::getVisitsMetricNames() VisitsSummary_CoreMetrics，否则使用 _ 前一个作为 PluginName

getDoneStringForPlugin($plugin):



$collection = Archive\DataCollection($names, 'numeric', $idsite, $period);
$archiveIds = $archive->getArchiveIds($names);

$names 应使用 PluginName_metric_name 命名


Archiver:

processor Piwik\ArchiveProcessor
logAggregator
params

$query = logAggregator->generateQuery($select, $from, $where, $groupBy, $orderBy)
$query = [
'sql' => $sql,
'bind' => $bind
],
bind => [start, end, sites]

Segment: Piwik\Segment
SegmentExpression


plugins/Actions/Archiver.php
plugins/Contents/Archiver.php
plugins/CustomDimensions/Archiver.php
plugins/CustomVariables/Archiver.php
plugins/DevicePlugins/Archiver.php
plugins/DevicesDetection/Archiver.php
plugins/Events/Archiver.php
plugins/ExamplePlugin/Archiver.php
plugins/Goals/Archiver.php
plugins/MobileAnalytics/Archiver.php
plugins/Provider/Archiver.php
plugins/Referrers/Archiver.php
plugins/Resolution/Archiver.php
plugins/UserCountry/Archiver.php
plugins/UserLanguage/Archiver.php
plugins/VisitTime/Archiver.php
plugins/VisitorInterest/Archiver.php
