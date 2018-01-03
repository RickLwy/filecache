<?php
class FileCache{
    private $file_name;
    public function __construct($file_name)
    {
        $this->file_name=$file_name;
    }
    public function load(){
        if(file_exists($this->file_name)){
            $content=file_get_contents($this->file_name);
            if(count($content)>0){
                return json_decode($content,true);
            }
        }
        return array();
    }
    public function setValue($name,$value,$time=null){
        $data=$this->load();
        if(isset($data[$name])){
            $data[$name]['value']=$value;
            $data[$name]['time']=($time==null)?null:time()+$time;
        }else{
            $data[$name]=['value'=>$value,'time'=>($time==null)?null:time()+$time];
        }
        file_put_contents($this->file_name,json_encode($data));
    }
    public function getValue($name){
        $data=$this->load();

        if(isset($data[$name])&&($data[$name]['time']>time()||$data[$name]['time']==null)){

           // pd($data[$name]['value']);
            return $data[$name]['value'];
        }
        return '';
    }
    public function flush(){
        file_put_contents($this->file_name,'');
    }
    public function delValue($name){
        $data=$this->load();
        if(isset($data[$name])){
            //pd($data);
            unset($data[$name]);

            //pd($data);
        }

    }
}
function pd($params){
    echo '<pre>';
    print_r($params);
    die;
}
$file_name=__DIR__.'/cache.txt';
$cache=new FileCache($file_name);
//$cache->setValue('qwe','123',200);
//$cache->setValue('lwy','qwe',10);

//echo $cache->getValue('qwe');
//$cache->flush();
//echo $cache->delValue('qwe');
//echo $cache->getValue('qwe');
