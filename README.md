Base-de-datos-30-05-14
======================

base de datos clase 30-05-14
use VENTASCIB

select *from TB_CLIENTE
order by RAZ_SOC_CLI asc, RUC_CLI desc
go

select *from TB_VENDEDOR
where COD_VEN in ('V01','V08','V10')
order by FEC_ING desc
go

select COD_VEN as 'CODIGO VENDEDOR',NOM_VEN as'NOMBRE VENDEDOR',APE_VEN as 'APELLIDO VENDEDOR',COD_DIS as ' CODIGO DISTRITO' from TB_VENDEDOR
where APE_VEN like 'O%'


select *from TB_PRODUCTO
where (PRE_PRO between 1 and 20) and (DES_PRO like '[A-D]%')

select RAZ_SOC_CLI, FEC_REG from TB_CLIENTE
where year (FEC_REG)=2011

select *from TB_CLIENTE
where year(FEC_REG) between 2011 and 2013  

select *from TB_FACTURA
where month(FEC_FAC) between 01 and 03

select *from TB_CLIENTE
where COD_CLI = 'C020'


update TB_CLIENTE 
set FEC_REG=getdate() 
where COD_CLI='C020'


// nueva consulta creando variables almacenadas en tablas

use VENTASCIB

declare @precio MONEY
set @precio=30
select *from TB_PRODUCTO
where PRE_PRO > @precio

declare @precio01 money, @precio02 money
set @precio01=10
set @precio02=50
select *from TB_PRODUCTO where PRE_PRO between @precio01 and @precio02

declare @variable varchar(5)
set @variable='SOTO'
select *from TB_VENDEDOR where APE_VEN = @variable


create procedure SP_CLIENTE_DISTRITO
@distrito char(5)
as
select*from TB_CLIENTE 
where COD_DIS =@distrito

exec SP_CLIENTE_DISTRITO 'D10'
