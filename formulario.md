<?php
include_once("ControladorBD.php");

session_start();
if (isset($_POST))
try
{
    if (($_POST))
    {
        $objetoNegocio=new ControladorBD($_POST["codigo"],$_POST["fecha"],$_POST["cuenta"],$_POST["movimiento"],$_POST["valor"]);

        if (isset($_POST["insertar"] ) )
        {
            $objetoNegocio->insertar();
        }
        if (isset($_POST["eliminar"] ) )
        {
            $objetoNegocio->eliminar();
        }
        if (isset($_POST["actualizar"] ) )
        {
            $objetoNegocio->actualizar();
        }
        if (isset($_POST["consultar"] ) )
        {
            $objetoNegocio->listar();
             
        }
        
    }
}
catch(PDOException $ex)
{
    echo $ex->getMessage() ;
}
?>
<!DOCTYPE html>
<html>
  <head>

    </style>
  <meta charset='utf-8'>
    
  </head>
  <body>
    <div id='contenido'>
      <header>
        <hgroup>
          <center><h1>Cuenta Bancaria "KAPAEL"</h1></center>
        </hgroup>
        
      </header>
      <section>
      
      <div id='textPr'>
          <article>
            <hgroup>
              <center><img src="imagen/images.jpg" /></center>
            
            </hgroup>
            
          </article>

<form action="formulario.php" method="post">
<center>
    
        
            
        
           <table>
           <tr>
                  <td> Codigo: </td>
                  <td> <input type="number" id="codigo" name="codigo" readonly="codigo" 
                    value="<?php if (isset($_POST["consultar"] ) ) echo $objetoNegocio->codigo;  ?>" />
                    </td>   

              </tr>

              <tr>
                  <td> Fecha: </td>
                  <td> <input type="date" id="fecha" name="fecha" autofocus required
                    value="<?php if (isset($_POST["consultar"] ) ) echo $objetoNegocio->fecha;  ?>" />
                    </td>   

              </tr>
              <tr>
                  <td> Cuenta: </td>
                  <td> <input type="text" id="cuenta" name="cuenta" 
                  value="<?php if (isset($_POST["consultar"] ) ) echo $objetoNegocio->cuenta;  ?>" />
                  </td>

              </tr>
              

<tr>
                  <td> Tipo Movimiento: </td>
                   <td> <select id ="movimiento" name="movimiento"    
                  value="<?php if (isset($_POST["consultar"] ) ) echo $objetoNegocio->movimiento;  ?>" />
      
          
            <option value="0">Seleccionar Movimiento</option>
            <option value="Deposito">Depósito</option>
            <option value="Retiro">Retiro</option>
            <option value="N/C">Nota de Crédito</option>
            <option value="N/D">Nota de Débito</option>
          
          </select>
        </td>
                  </td>
              </tr>






              <tr>
                  <td> valor: </td>
                  <td> <input type="text" id = "valor" name="valor"  min="1" 
                  value="<?php if (isset($_POST["consultar"] ) ) echo $objetoNegocio->valor;  ?>" />

                  </td>
              </tr>
              
              
              </table>      
    </table> 

    <table> 
        
            <tr>
                <td><input type="submit" id="insertar" name="insertar" value="Insertar" /></td>
                <td><input type="submit" id="eliminar" name="eliminar" value="Eliminar" /></td>
                <td><input type="submit" id="actualizar" name="actualizar" value="Actualizar" /></td>
                <td><input type="submit" id="consultar" name="consultar" value="Consultar" /></td>
            </tr>
        </div>
    </table> 
</center>    
</form>
</div>
	</div>
			</section>
		
		<footer>
			<canvas id='miCanvas'>
			</canvas>
		</footer>		
	</body>
</html>