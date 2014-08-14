<?php
include_once("Modelo.php");

class ControladorBD
{
    public $codigo;
    public $fecha;
    public $cuenta;
    public $movimiento;
    public $valor;

    public function __construct($codigo,$fecha,$cuenta,$movimiento,$valor)
    {
        $this->codigo=$codigo;
        $this->fecha=$fecha;
        $this->cuenta=$cuenta;
        $this->movimiento=$movimiento;
        $this->valor=$valor;

        $this->objetoDatos=new Modelo('mysql:host=localhost;port=3306;dbname=cup-cake','root','');
    }
    public function insertar()
    {
        try
        {
            $this->objetoDatos->conectar();
            $this->objetoDatos->ejecutar("insert into banco (codigo,fecha,cuenta,movimiento,valor)
             values('$this->codigo', '$this->fecha','$this->cuenta', '$this->movimiento','$this->valor')");
             $this->objetoDatos->desconectar();   
             
        }

        
        catch (PDOException $ex)
        {
            throw $ex;
        }

    }


    public function eliminar()
    {
        try
        {
        $this->objetoDatos->conectar();
        $this->objetoDatos->ejecutar("delete from banco where cuenta='$this->cuenta' ");
        $this->objetoDatos->desconectar();
    
     }
        catch (PDOException $ex)
        {
            throw $ex;
        }
    }
    public function actualizar()
    {
        try
        {
        $this->objetoDatos->conectar();
        $this->objetoDatos->ejecutar("update banco set  valor=$this->valor where cuenta=$this->cuenta");
        $this->objetoDatos->desconectar();
    }
    catch (PDOException $ex)
        {
            throw $ex;
        }
    }
    public function listar()
    {
        try
        {
        $this->objetoDatos->conectar();
        $rs=$this->objetoDatos->ejecutar("select sum('valor') from banco  where cuenta=$this->cuenta and movimiento='$this->movimiento'");

/*SELECT SUM( valor ) 
FROM banco
WHERE movimiento =  "deposito"
AND cuenta =1212
*/

        if (count($rs))
        {
            //$this->codigo=$rs[0]['codigo'];
            //$this->fecha= $rs[0]['fecha'];
            //$this->cuenta= $rs[0]['cuenta'];
           // $this->movimiento= $rs[0]['movimiento'];
            $this->valor= $rs[0]['valor'];
        }
        $this->objetoDatos->desconectar();
    }
    catch (PDOException $ex)
        {
            throw $ex;
        }
    
}
}

?>