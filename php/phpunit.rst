PHPUnit
==============================

DataProvider
------------------------------

使用 dataProvider ::

    /**
     * @dataProvider dataProvider
     */
    public function testValidate($value, $result)
    {
        $this->validation->add('int', new Integer());
        $errors = $this->validation->validate(['int' => $value]);
        $this->assertEquals(count($errors), $result ? 0 : 1);
    }

    public function dataProvider()
    {
        return [
            [123, true],
            ['123', true],
            ['-123', true],
            ['+123', true],
            ['a', false]
        ];
    }


Mock 不使用原始构造函数
------------------------------

disableOriginalConstructor 禁用原始构造函数 ::

    $mock = $this->getMockBuilder('class_name')
        ->disableOriginalConstructor()
        ->getMock();

http://www.phpunit.de/manual/current/en/test-doubles.html

Mock 多次调用返回值
------------------------------

onConsecutiveCalls 设置连续调用的返回值 ::

        $stub->expects($this->any())
             ->method('doSomething')
             ->will($this->onConsecutiveCalls(2, 3, 5, 7));

Mock 多次调用参数
------------------------------

使用 at 设置每次调用的值 ::

       $mock->expects($this->at(0))
             ->method('exists')
             ->with($this->equalTo('foo'))
             ->will($this->returnValue(true));

        $mock->expects($this->at(1))
             ->method('exists')
             ->with($this->equalTo('bar'))
             ->will($this->returnValue(false));

Mock 返回值使用回调函数
------------------------------

使用 returnCallback ::

       $context->expects($this->exactly(2))
           ->method('offsetGet')
           ->with($this->logicalOr(
                     $this->equalTo('Matcher'), 
                     $this->equalTo('Logger')
            ))
           ->will($this->returnCallback(
                function($param) {
                    var_dump(func_get_args());
                    // The first arg will be Matcher or Logger
                    // so something like "return new $param" should work here
                }
           ));

dataProvider
------------------------------

::

    class DataTest extends PHPUnit_Framework_TestCase
    {
        /**
         * @dataProvider additionProvider
         */
        public function testAdd($a, $b, $expected)
        {
            $this->assertEquals($expected, $a + $b);
        }
    
        public function additionProvider()
        {
            return array(
              array(0, 0, 0),
              array(0, 1, 1),
              array(1, 0, 1),
              array(1, 1, 3)
            );
        }
    }

