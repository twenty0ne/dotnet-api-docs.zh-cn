### <a name="reflection-objects-can-no-longer-be-passed-from-managed-code-to-out-of-process-dcom-clients"></a>反射对象无法再从托管代码向进程外 DCOM 客户端传递

|   |   |
|---|---|
|详细信息|反射对象可能无法再从托管代码传道至进程外客户端 以下类型将受影响：<ul><li><xref:System.Reflection.Assembly?displayProperty=name></li><li><xref:System.Reflection.MemberInfo?displayProperty=name> (及其派生类型，包括<xref:System.Reflection.FieldInfo?displayProperty=name>， <xref:System.Reflection.MethodInfo?displayProperty=name>， <xref:System.Type?displayProperty=name>，和<xref:System.Reflection.TypeInfo?displayProperty=name>)</li><li><xref:System.Reflection.MethodBody?displayProperty=name></li><li><xref:System.Reflection.Module?displayProperty=name></li><li><xref:System.Reflection.ParameterInfo?displayProperty=name>。</li></ul>调用对象的 <code>IMarshal</code> 会返回 <code>E_NOINTERFACE</code>。|
|建议|更新封送代码，以与非反射对象一起使用|
|范围|次要|
|版本|4.6|
|类型|运行时|
