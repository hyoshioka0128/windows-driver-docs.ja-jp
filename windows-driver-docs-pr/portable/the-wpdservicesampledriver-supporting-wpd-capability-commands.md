---
Description: 機能のコマンド (WpdServiceSampleDriver サンプル) のサポート
title: 機能のコマンド (WpdServiceSampleDriver サンプル) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3125c92465bc90d9f60816239ca6ed3301ed1dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370487"
---
# <a name="support-for-capability-commands-wpdservicesampledriver-sample"></a>機能のコマンド (WpdServiceSampleDriver サンプル) のサポート


ドライバーのサンプルでは、サービスのデバイスの 10 の機能コマンドおよび 14 の機能のコマンドをサポートします。 デバイスの機能のコマンドをサポートするコードは「 *WpdCapabilities.cpp*します。 サービス機能のコマンドをサポートするコードは「 *WpdServiceCapabilities.cpp*します。 WPD は、アプリケーションがデバイスの機能またはサービス機能のデータを取得するときに、これらのコマンドを呼び出します。 たとえば、アプリケーションを呼び出すと**IPortableDeviceServiceCapabilities::GetSupportedFormats**、WPD 問題の対応する WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_形式ドライバーにコマンドを特定のサービスのサポートされている形式を取得します。

## <a name="span-idthedevice-capabilitycommandsspanspan-idthedevice-capabilitycommandsspanspan-idthedevice-capabilitycommandsspanthe-device-capability-commands"></a><span id="The_Device-Capability_Commands"></span><span id="the_device-capability_commands"></span><span id="THE_DEVICE-CAPABILITY_COMMANDS"></span>デバイスの機能のコマンド


アプリケーションを呼び出すいくつかのメソッドのいずれかに、デバイスの機能のコマンドが発行された、 **IPortableDeviceCapabilities**インターフェイス。 これらのコマンドが最初に、処理、 **WpdCapabilities::DispatchMessage**をさらに、対応するコマンド ハンドラーを呼び出すメソッド。 **DispatchMessage**メソッドと個別のハンドラーは、「、 *WpdCapabilities.cpp*ファイル。次の表では、デバイス機能のコマンド ハンドラーの名前とのそれぞれについて説明しますが**DispatchMessage**特定のコマンドを処理するときに呼び出します。

| コマンド                                                            | ハンドラー                        | 説明                                                                                                                                  |
|--------------------------------------------------------------------|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_機能\_取得\_サポートされている\_コマンド               | OnGetSupportedCommands         | デバイスでサポートされているコマンドのセットを取得しようとするアプリケーションに発行されます。                                           |
| WPD\_コマンド\_機能\_取得\_コマンド\_オプション                  | OnGetCommandOptions            | 特定のコマンドでサポートされているオプションを取得する際に、アプリケーションを発行します。                                              |
| WPD\_コマンド\_機能\_取得\_サポートされている\_機能\_カテゴリ | OnGetFunctionalCategories      | デバイスでサポートされている機能のカテゴリのセットを取得しようとするアプリケーションに発行されます。                              |
| WPD\_コマンド\_機能\_取得\_機能\_オブジェクト               | OnGetFunctionalObjects         | 特定の機能カテゴリでサポートされている機能のオブジェクトのセットを取得しようとするアプリケーションに発行されます。                |
| WPD\_コマンド\_機能\_取得\_サポートされている\_コンテンツ\_型         | OnGetSupportedContentTypes     | 特定の機能カテゴリでサポートされているコンテンツの種類を取得しようとするアプリケーションに発行されます。                            |
| WPD\_コマンド\_機能\_取得\_サポートされている\_書式設定                | OnGetSupportedFormats          | アプリケーションの特定のコンテンツ タイプでサポートされている形式のセットを取得しようとするときに発行します。                                  |
| WPD\_コマンド\_機能\_取得\_サポートされている\_形式\_プロパティ     | OnGetSupportedFormatProperties | 指定した形式でサポートされているプロパティのセットを取得しようとするアプリケーションに発行されます。                                     |
| WPD\_コマンド\_機能\_取得\_固定\_プロパティ\_属性       | OnGetFixedPropertyAttributes   | アプリケーションが同一 (または固定) のプロパティ属性のセットを取得しようとするときに発行された、特定形式のすべてのオブジェクト。 |
| WPD\_コマンド\_機能\_取得\_イベント\_オプション                    | OnGetEventOptions              | 特定のイベントに関連付けられているオプションを取得する際に、アプリケーションを発行します。                                             |
| WPD\_コマンド\_機能\_取得\_サポートされている\_イベント                 | OnGetSupportedEvents           | デバイスでサポートされているイベントのセットを取得しようとするアプリケーションに発行されます。                                               |

 

## <a name="span-idtheservice-capabilitycommandsspanspan-idtheservice-capabilitycommandsspanspan-idtheservice-capabilitycommandsspanthe-service-capability-commands"></a><span id="The_Service-Capability_Commands"></span><span id="the_service-capability_commands"></span><span id="THE_SERVICE-CAPABILITY_COMMANDS"></span>サービス機能のコマンド


サービス機能のコマンドは、アプリケーションがいくつかのメソッドのいずれかを呼び出すときに発行された、 **IPortableDeviceServiceCapabilities**インターフェイス。 これらのコマンドが最初に、処理、 **WpdServiceCapabilities::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、「、 *WpdServiceCapabilities.cpp*ファイル。次の表では、デバイス機能のコマンド ハンドラーの名前とのそれぞれについて説明しますが**DispatchMessage**特定のコマンドを処理するときに呼び出します。

| コマンド                                                                     | ハンドラー                        | 説明                                                                                                            |
|-----------------------------------------------------------------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_コマンド               | OnGetSupportedCommands         | 特定のサービスでサポートされているコマンドのセットを取得しようとするアプリケーションに発行されます。              |
| WPD\_コマンド\_サービス\_機能\_取得\_コマンド\_オプション                  | OnGetCommandOptions            | 特定のコマンドでサポートされているオプションを取得する際に、アプリケーションを発行します。                        |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_メソッド                | OnGetSupportedMethods          | 特定のサービスでサポートされているメソッドを取得しようとするアプリケーションに発行されます。                      |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_メソッド\_BY\_形式    | OnGetSupportedMethodsByFormat  | 特定のサービスで、特定の形式でサポートされているメソッドを取得しようとするアプリケーションに発行されます。    |
| WPD\_コマンド\_サービス\_機能\_取得\_メソッド\_属性                | OnGetMethodAttributes          | 特定のメソッドの属性を取得しようとするアプリケーションに発行されます。                                        |
| WPD\_コマンド\_サービス\_機能\_取得\_メソッド\_パラメーター\_属性     | OnGetMethodParameterAttributes | 特定のメソッド パラメーターの属性を取得しようとするアプリケーションに発行されます。                              |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_機能\_カテゴリ | OnGetFunctionalCategories      | 特定のサービスでサポートされている機能のカテゴリのセットを取得しようとするアプリケーションに発行されます。 |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_書式設定                | OnGetSupportedFormats          | 特定のサービスでサポートされている形式を取得しようとするアプリケーションに発行されます。                        |
| WPD\_コマンド\_サービス\_機能\_取得\_形式\_属性                | OnGetFormatAttributes          | サービスでサポートされている特定の形式の属性を取得しようとするアプリケーションに発行されます。        |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_形式\_プロパティ     | OnGetSupportedFormatProperties | 指定した形式でサポートされているプロパティのセットを取得しようとするアプリケーションに発行されます。               |
| WPD\_コマンド\_サービス\_機能\_取得\_形式\_プロパティ\_属性      | OnGetFormatPropertyAttributes  | サービスの特定の形式のプロパティの属性のセットを取得しようとするアプリケーションに発行されます。         |
| WPD\_コマンド\_サービス\_機能\_取得\_サポートされている\_イベント                 | OnGetSupportedEvents           | 特定のサービスでサポートされているイベントを取得しようとするアプリケーションに発行されます。                       |
| WPD\_コマンド\_サービス\_機能\_取得\_イベント\_属性                 | OnGetEventAttributes           | サービスの特定のイベントの属性を取得しようとするアプリケーションに発行されます。                          |
| WPD\_コマンド\_サービス\_機能\_取得\_イベント\_パラメーター\_属性      | OnGetEventParameterAttributes  | サービスの特定のイベントのパラメーターの属性を取得しようとするアプリケーションに発行されます。                |
| WPD\_コマンド\_サービス\_機能\_取得\_継承された\_サービス               | OnGetInheritedServices         | 特定のサービスによって継承されるサービスを取得する際に、アプリケーションを発行します。                     |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





