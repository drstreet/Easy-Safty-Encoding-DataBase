# Easy-Safty-Encoding-DataBase
Easy &amp; Safty Encoding DataBase With Laravel


Route::get('/tableconvertor/{table}' ,['middleware'=>'Auth' , function($table){

        $fields = DB::select("DESCRIBE {$table}");
        foreach ($fields as $field ){
            if(substr($field->Type, 0 , 7)  == "varchar"){
                $num=substr(explode('(',$field->Type)[1],0,-1);
                DB::transaction(function() use($table,$field,$num) {
                    DB::statement("alter table {$table} change $field->Field $field->Field VARBINARY($num);");
                    DB::statement("alter table {$table} change $field->Field $field->Field $field->Type  CHARACTER SET utf8mb4;");
                });
            }
        }
        dd('DONE:    ' . $table);
    }]);
    
    Example  :   http://yoursites.com/tableconvertor/TABLENAME
    
    
