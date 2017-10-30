# LisModel class

#### 简介

``` php
final LisModel {
	protected static object $_pdo;
	protected string $_dns;
	protected string $_username;
	protected string $_password;
	protected array $_option;
	
	public function __construct($dbConfig);
	public function pdo();
	public function table(string $tableName);
	public function selectTable(string $tableName);
	public function columns(array $columns);
	public function where(array $where);
	public function getSql();
	public function group(array $group);
	public function order(array $order);
	public function query();
	public function prepare(string $sql);
	public function leftJoin(array $join);
	public function rightJoin(array $join);
	public function fullJoin(array $join);
	public function innerJoin(array $join);
	public function insert(array $insertData);
	public function update(array $updateData, array $where);
	public function delete(array $where);
}
```

#### 案例

``` php
<?php
\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();
$dbconfig = [
    "test_db" => [

            'dns' => 'mysql:host=127.0.0.1;dbname=test',
            'username' => 'root',
            'password' => '123456',
 
            //PDO驱动选项
            'option' => [
                PDO::ATTR_CASE => PDO::CASE_NATURAL
            ]  
    ]  
];
\Lis\Config::load($dbconfig);

class TestModel extends \Lis\Model {
    public $table = "test";
    public function __construct() {
        parent::__construct(LisConfig::get('test_db'));
    }

    public function testFunc() {

        //select id * from test
        $query = $this->table('test')->columns(['id'])->query();
        $info = $query->fetchAll();

        //select * from test as u
        $this->table('user as u')->columns('*')->query();

        //select u.id,u.name from user as u 
        $this->table('user as u')->columns(['u.id','u.name']);

        //SELECT id,name FROM test WHERE age=22 AND age2=33 AND name='test' AND age IN (1,10) AND age>21 AND age>=20 AND age<=21 AND age<22 AND age!=22.333 AND name LIKE '%test%' AND age IN (1,10) AND age NOT IN (1,10) AND name NOT IN ('aaa','bbb') AND age BETWEEN 1 AND 10 AND name NOT BETWEEN 'aaa' AND 'bbb' OR ( age BETWEEN 1 AND 10 AND AND age NOT BETWEEN 1 AND 10 OR age IN (1,10))  GROUP BY id,name  ORDER BY id DESC, name ASC 
        $this->columns(['id','name'])->where([
            'age' => 22,
            'age2' => 33,
            'name[=]' => 'test',  
            '[AND]' => [ 'age[!]' => [1, 10] ],  
            'age[>]' => 21,  
            'age[>=]' => 20,  
            'age[<=]' => 21,  
            'age[<]' => 22,  
            'age[!=]' => 22.333,  
            'name[%]' => '%test%',                  //LIKE %%
            'age[!]' => [1, 10],                    //IN (, 10)
            'age[~!]' => [1, 10],                   // NOT IN (1, 10)
            'name[~!]' => ["aaa", "bbb"],           
            'age[<>]' => [1, 10],                   //BETWEEN 
            'name[><]' => ['aaa', 'bbb'],           //NOT BETWEEN
            '[OR]' => [                                                                                                                            
                'age[<>]' => [1, 10],                                                                                    
                '[AND]' => [  
                    '[age!]' => [2, 10] 
                ], 
                'age[><]' => [1, 10],
                '[OR]' => [  
                    'age[!]' => [1, 10] 
                ], 
            ],  
        ])->group(['id', 'name'])->order(['id' => 'DESC', 'name' => 'ASC']);

        var_dump($this->getSql());

        //返回PDO对象
        var_dump($this->pdo()); 
        
        //join: leftJoin rightJoin fullJoin innerJoin
        $c1 = $this->table('test as a')->columns(['a.id', 'b.id'])->innerJoin([                                                                    
            'test1 as b' => ['a.id' => 'b.id'],                                                                                                    
        ])->where([                                                                                                                                
            'a.id' => 1,                                                                                                                           
        ])->query();                   
       
        //自定义SQL
        $this->pdo()->prepare('select * from test');
        $sth->execute();
        var_dump($sth->fetchAll(PDO::FETCH_COLUMN|PDO::FETCH_GROUP)); 


        //事务
        try{

            $this->pdo()->beginTransaction();

            //insert
            $this->table('test')->insert(
                ['id' => 14, 'name' => 'test'] 
            );
            echo 'last id = '. $this->pdo()->lastInsertId()."\n";
            $res = $this->table('test')->insert(
                ['id' => 6, 'third_corp_id' => 9] 
            );
            if ($res == false) {
                $this->pdo()->rollback();
                return;
            }
        } catch(Exception $e) {
            $this->pdo()->rollback();
            return;
        }
        $this->pdo()->commit();

        //update
        $res = $this->table('test')->update(
            ['name' => 'test'] ,
            ['id' => 1]
        );

        //切换表
        $this->selectTable('test1');

        //delete
        $res = $this->delete(['id' => 2]);

    }
}

$testModel = new TestModel();
$testModel->testFunc();

$app->run();
?>

```


