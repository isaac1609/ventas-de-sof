# Diagnóstico Supabase

Proyecto: `gixfexkbblslkrksnazw` (`https://gixfexkbblslkrksnazw.supabase.co`).

La consulta realizada el 15 de agosto de 2026 confirmó que `public.pelu_herramientas`, `public.pelu_alertas_herramientas` y `public.pelu_servicio_insumos` existían, pero no contenían registros. La tabla `pelu_herramientas` tenía columnas `id`, `nombre`, `tipo`, `precio_compra`, `fecha_compra`, `vida_util_total`, `cortes_realizados`, `costo_por_corte`, `porcentaje_vida_restante`, `alerta_mantenimiento`, `created_at`, `updated_at`. La migración aplicada creó `public.pel_herramientas` para la aplicación actual con `nombre`, `tipo`, `precio_compra`, `vida_util_total`, `cortes_realizados`, `alerta_mantenimiento`, `activo`, marcas de tiempo y políticas RLS para anon/authenticated.

Las ventas actuales usan `public.pel_registros_ventas`, los insumos usan `public.pel_insumos` y los productos usan `public.pel_productos`. La lógica pedida es: una venta de servicio descuenta insumos y herramientas; una venta de producto descuenta únicamente `pel_productos.stock`.

Advertencia de Supabase: varias tablas antiguas `pelu_*` tienen RLS desactivado según el asesoramiento del proyecto. No se activaron automáticamente porque hacerlo sin políticas puede bloquear el acceso. Referencia oficial: https://supabase.com/docs/guides/database/postgres/row-level-security

La migración `create_pel_herramientas` fue aplicada con políticas explícitas de SELECT, INSERT, UPDATE y DELETE para las sesiones actuales.
