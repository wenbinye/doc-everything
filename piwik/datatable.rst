row:
columns
metadata
subtable id 所属表ID

Manager: 所有 DataTable 有 ID，由 manager 分配

DataTable:
addRow(Row $row);
addRowsFromArray([
    [
        Row::COLUMNS => [],
        Row::METADATA => []
    ]
]);

$datatable->setMetadata($name, $value);

queueFilter($className, $params)
string|closure

applyQueuedFilters(); 应用过滤


ReplaceColumnNames 由 Metrics id 转换成 column_name


