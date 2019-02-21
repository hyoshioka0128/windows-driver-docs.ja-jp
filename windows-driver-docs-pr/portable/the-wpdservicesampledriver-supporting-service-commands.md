---
Description: Supporting the Service Commands
title: サービスのコマンドをサポートしています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27fba5e4e3e40acfd1fb9a82ea930678f248972c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538863"
---
# <a name="supporting-the-service-commands"></a>サービスのコマンドをサポートしています。


WPD は、アプリケーションが WPD API でサポートされているサービス インターフェイス内にあるいくつかのメソッドを呼び出すと、サービスのコマンドを発行します。

これらのサービスのコマンドをまずによって処理サンプル ドライバーで、 **WpdService::DispatchMessage**メソッド。 このメソッドは、特定のコマンドを調べ、適切なハンドラーに転送します。 ドライバーのサンプル転送の機能コマンドのハンドラーに、 *WpdServiceCapabilities.cpp*モジュール。 ドライバーのサンプルでは転送のハンドラー メソッドのコマンドのいずれか、 *WpdServiceMethods.cpp*モジュール。

次の表では、その説明およびハンドラーと共に、サービス モジュールでサポートされているコマンドについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">説明/ハンドラー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_START_INVOKE</td>
<td align="left"><p>説明:アプリケーションがいずれかを呼び出すときに発行、 <strong>IPortableDeviceServiceMethods::Invoke</strong>または<strong>IPortableDeviceServiceMethods::InvokeAsync</strong>メソッド。</p>
<p>ハンドラー:<strong>WpdServiceMethods::OnStartInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_METHODS_END_INVOKE</td>
<td align="left"><p>説明:アプリケーションによって呼び出された、メソッドの実行が終了に発行されます。 (WPD は、同期および非同期メソッドに対してこのコマンドを発行します)。</p>
<p>ハンドラー:<strong>WpdServiceMethods::OnEndInvoke</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_CANCEL_INVOKE</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行、 <strong>IPortableDeviceServiceMethods::Cancel</strong>メソッドが完了していないメソッドの呼び出しをキャンセルします。</p>
<p>ハンドラー:<strong>WpdServiceMethods::OnCancelInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_COMMON_GET_SERVICE_OBJECT_ID</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行、 <strong>IPortableDeviceService::GetServiceObjectId</strong>の現在のサービス オブジェクトの識別子を取得します。</p>
<p>ハンドラー:<strong>OnGetServiceObjectID</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupportingtheservice-capabilitycommandsspanspan-idsupportingtheservice-capabilitycommandsspanspan-idsupportingtheservice-capabilitycommandsspansupporting-the-service-capability-commands"></a><span id="Supporting_the_Service-Capability_Commands"></span><span id="supporting_the_service-capability_commands"></span><span id="SUPPORTING_THE_SERVICE-CAPABILITY_COMMANDS"></span>サービス機能のコマンドをサポートしています。


WPD アプリケーション内にあるメソッドを使用して、 **IPortableDeviceServiceCapabilities**インターフェイスには、サービスによって提供される機能です。 このインターフェイスのメソッドを使用すると、アプリケーションがサポートされているメソッド、イベント、および形式の説明を取得できます。 また、アプリケーションは、特定のメソッドの特定のパラメーターの属性などのさらに詳細なデータを取得できます。

サンプル ドライバーで、 **WpdService::DispatchMessage**メソッドは、検査、 **fmtid**フィールドのすべての着信コマンド。 WPD にこのフィールドが設定されている場合\_カテゴリ\_サービス\_コマンドを転送、機能、 **WpdServiceCapabilities::DispatchWpdMessage**さらに、コマンドを処理するメソッド。 (、 **WpdServiceCapabilities::DispatchWpdMessage**メソッドがある、 *WpdServiceCapabilities.cpp*ファイルです)。

次の表では、14 の機能のコマンドでサポートされている、 **WpdServiceCapabilities::DispatchWpdMessage**とその説明およびハンドラーのメソッド。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">説明/ハンドラー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_COMMANDS</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetSupportedCommands</strong>を現在のサービスのサポートされている WPD コマンドの一覧を取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedCommands</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_COMMAND_OPTIONS</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetCommandOptions</strong>現在のサービスによって実装されている任意の WPD コマンド オプションを取得します。</p>
<p>ハンドラー:<strong>OnGetCommandOptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetSupportedMethods</strong>オブジェクト形式の現在のサービスに適用されるサービス メソッドをサポートされているデバイスの一覧を取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedMethods</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS_BY_FORMAT</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetSupportedMethodsByFormat</strong>オブジェクト形式の現在のサービスに適用されるサービス メソッドをサポートされているデバイスの一覧を取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedMethodsByFormat</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetMethodAttributes</strong>デバイス サービス メソッドの属性 (たとえば、名とパラメーター) を取得します。</p>
<p>ハンドラー:<strong>OnGetMethodAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetMethodParameterAttributes</strong>を特定のデバイスのサービス メソッドのパラメーターの属性 (たとえば、名と VARTYPE) を取得します。</p>
<p>ハンドラー:<strong>OnGetMethodParameterAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMATS</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetSupportedFormats</strong>現在のサービスのための形式、サポートされているオブジェクトを取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedFormats</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetFormatAttributes</strong>メソッド。</p>
<p>ハンドラー:<strong>OnGetFormatAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行、 <strong>IPortableDeviceServiceCapabilities::GetSupportedFormatProperties</strong>特定の形式のサポートされているプロパティの一覧を取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedFormatProperties</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_PROPERTY_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetFormatPropertyAttributes</strong>プロパティの属性 (たとえば、名前、フォーム、VARTYPE) を取得します。</p>
<p>ハンドラー:<strong>OnGetFormatPropertyAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_EVENTS</td>
<td align="left"><p>説明:ときにアプリケーション呼び出しを発行<strong>IPortableDeviceServiceCapabilities::GetSupportedEvents</strong>を現在のサービスのサポートされているイベントの一覧を取得します。</p>
<p>ハンドラー:<strong>OnGetSupportedEvents</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetEventAttributes</strong>デバイス サービス イベントの属性 (名、パラメーターなど) を取得します。</p>
<p>ハンドラー:<strong>OnGetEventAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetEventParameterAttributes</strong>特定のイベント パラメーターの属性を取得します。</p>
<p>ハンドラー:<strong>OnGetEventParameterAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_INHERITED_SERVICES</td>
<td align="left"><p>説明:アプリケーションを呼び出すときに発行<strong>IPortableDeviceServiceCapabilities::GetInheritedServices</strong>の現在のサービスによって実装される抽象サービスを取得します。</p>
<p>ハンドラー:<strong>OnGetInheritedServices</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupportingthewpdcommandservicemethodsstartinvokecommandspanspan-idsupportingthewpdcommandservicemethodsstartinvokecommandspanspan-idsupportingthewpdcommandservicemethodsstartinvokecommandspansupporting-the-wpdcommandservicemethodsstartinvoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_start_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_COMMAND"></span>WPD をサポートしている\_コマンド\_サービス\_メソッド\_開始\_INVOKE コマンド


WPD アプリケーションが含まれる 2 つのメソッドのいずれかを呼び出すことによって、特定のサービスでサポートされているメソッドを呼び出す、 **IPortableDeviceServiceMethods**インターフェイス。 **IPortableDeviceServiceMethods::Invoke**メソッドが同期中にメソッドを呼び出す、 **IPortableDeviceServiceMethods::InvokeAsync**メソッドが特定のメソッドを非同期的に呼び出します。

をアプリケーションがこれら 2 つのメソッドのいずれかを呼び出すと WPD API では、のさらに、問題 WPD\_コマンド\_サービス\_メソッド\_開始\_ドライバーに INVOKE コマンド。

ドライバーのサンプル、WPD で\_コマンド\_サービス\_メソッド\_開始\_内にある次の表に、メソッド呼び出しでコマンドの結果を呼び出し、 *WpdServiceMethods.cpp*モジュール。

| メソッド名                          | 説明                                                                                                                                                                                                           |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnStartInvoke** | 呼び出し、 **StartMethod**ヘルパー関数を完了すると、呼び出されたメソッドのコンテキストを返します、 **IPortableDeviceValues**オブジェクト。                                                                           |
| **WpdServiceMethods::StartMethod**   | 特定のサービスが要求されたメソッドをサポートしている場合は、新たに作成であることを検証**ServiceMethodContext**オブジェクト。 コンテキストが作成された後、 **ServiceMethodContext::Initalize**メソッドが呼び出されます。 |
| **ServiceMethodContext::Initialize** | 作成、 **CMethodTask**オブジェクトとなり、 **CMethodTask::Run**メソッド。                                                                                                                                         |
| **CMethodTask::Run**                 | 呼び出されたメソッドの実行に使用できる別のスレッドを作成します。                                                                                                                                                        |

 

ときに、 **WpdServiceMethods::OnStartInvoke**メソッドが呼び出されると、WPD が呼び出されるメソッドの GUID 識別子を渡します。 この GUID は、データを渡された、 *pParams*引数ポイント。

サポートされているメソッドの Guid がある、 *ContactDeviceService.h*と*FullEnumSyncDeviceService.h*ヘッダー ファイル。

メソッドのコンテキストは、ドライバーと WPD 識別し、ターゲットの特定のメソッドの呼び出しに使用する文字列です。 たとえば、WPD は、指定されたメソッドの特定の呼び出しをキャンセルする、またはそのメソッドの完了を通知するコマンドを発行するとき、この文字列を使用します。

## <a name="span-idsupportingthewpdcommandservicemethodsendinvokecommandspanspan-idsupportingthewpdcommandservicemethodsendinvokecommandspanspan-idsupportingthewpdcommandservicemethodsendinvokecommandspansupporting-the-wpdcommandservicemethodsendinvoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_end_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_COMMAND"></span>WPD をサポートしている\_コマンド\_サービス\_メソッド\_エンド\_INVOKE コマンド


ドライバーが、WPD を送信するメソッドが完了したら、\_イベント\_サービス\_WPD API への完全なイベント。 イベント データには、そのメソッドが呼び出されたときに、ドライバーが作成されたメソッドのコンテキストが含まれています。 このイベント通知を受信すると、WPD API の問題、WPD\_コマンド\_サービス\_メソッド\_エンド\_コマンドを呼び出すし、メソッドのコンテキストで次のコマンドが含まれています。 結果内にある次のメソッド呼び出しで、ドライバーのサンプルでは、このコマンドを受信すると*WpdServiceMethods.cpp*します。

| メソッド名                        | 説明                                                                                                                                                                                                                   |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnEndInvoke** | 呼び出し、 **EndMethod**ヘルパー関数を完了すると、呼び出されたメソッドの結果とステータス コードを返します。 このメソッドはまた、メソッドのコンテキストに関連付けられているリソースのクリーンアップするのに必要なを実行します。 |
| **WpdServiceMethods::EndMethod**   | 呼び出されたメソッドの結果とステータス コードを取得します.                                                                                                                                                                      |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





