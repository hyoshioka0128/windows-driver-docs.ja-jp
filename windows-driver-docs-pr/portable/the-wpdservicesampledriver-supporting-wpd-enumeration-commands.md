---
Description: Support for enumeration commands (WpdServiceSampleDriver)
title: 列挙型のコマンド (WpdServiceSampleDriver) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee7271f82d41f60408f886682f1b2484adde82f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528675"
---
# <a name="support-for-enumeration-commands-wpdservicesampledriver"></a>列挙型のコマンド (WpdServiceSampleDriver) のサポート


ドライバーのサンプルでは、列挙体の 3 つのコマンドをサポートします。 これらのコマンドが最初に、処理、 **WpdObjectEnumerator::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、すべてで、 *WpdObjectEnum.cpp*ファイル。

各列挙要求は、特定のアプリケーションが受け取るアクセス スコープを識別する列挙体コンテキストに関連付けられます。 たとえばを呼び出すアプリケーション**IPortableDevice::Open**デバイス全体のアクセスを備え、アプリケーションが呼び出し中に、階層内のすべてのオブジェクトを受け取る**IPortableDeviceService::Open**サービス レベルのアクセスを備え、デバイス オブジェクト、サービス オブジェクト、およびサービスのオブジェクト階層内のすべての子のみを受け取ります。

次の表は、ハンドラーの名前と共に、サポートされている列挙型のコマンドのそれぞれを**DispatchMessage**特定のコマンドを処理するときに呼び出します。 これらのコマンドが発行されるは、アプリケーションがいくつかのメソッドのいずれかを呼び出すときに、 **IPortableDeviceContent**または**IEnumPortableDeviceObjectIDs**インターフェイス。

| コマンド                                        | ハンドラー     | 説明                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD\_コマンド\_オブジェクト\_列挙\_開始\_検索 | OnStartFind | 新しい列挙体の内容を作成し、クライアントのコンテキスト マップに格納します。 |
| WPD\_コマンド\_オブジェクト\_列挙\_検索\_[次へ]  | 派生  | 要求されたオブジェクトのオブジェクト識別子を返します。                     |
| WPD\_コマンド\_オブジェクト\_列挙\_エンド\_検索   | OnEndFind   | 列挙が完了すると、必要なクリーンアップを実行します。               |

 

ドライバーのサンプル コード、WPD をそのままの\_コマンド\_オブジェクト\_列挙\_エンド\_WpdHellowWorldDriver サンプルに含まれるコードとほぼ同じハンドラーを検索します。 ただし、WPD のコードの一部を変更しました\_コマンド\_オブジェクト\_列挙\_開始\_検索と WPD\_オブジェクト\_列挙\_検索\_サービス レベルのアクセスをサポートするために次のハンドラー。

## <a name="span-idwpdcommandobjectenumerationstartfindspanspan-idwpdcommandobjectenumerationstartfindspanwpdcommandobjectenumerationstartfind"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD\_COMMAND\_OBJECT\_ENUMERATION\_START\_FIND


ドライバーの呼び出し、 **WpdObjectEnumerator::OnStartFind** WPD への応答ハンドラー\_コマンド\_オブジェクト\_列挙\_開始\_検索コマンド。 ハンドラーがさらに、作成、初期化、およびクライアント コンテキスト マップに新しい列挙体の内容を追加します。

サンプル ドライバーの場合は、各クライアントの列挙要求は、列挙型のコンテキストに関連付けられてとこのコンテキストはそのクライアントのアクセス スコープを識別します。

```ManagedCPlusPlus
        if (pEnumeratorContext != NULL)
        {
            ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
            m_pDevice->InitializeEnumerationContext(Scope, wszParentID, pEnumeratorContext);

            // Add the enumeration context to the client context map.  This calls AddRef() on pEnumeratorContext
            hr = pContextMap->Add(pEnumeratorContext, strEnumContext);
            CHECK_HR(hr, "Failed to add the enumeration context");
        }
```

アクセス スコープとその用途の詳細については、次を参照してください。、[プロパティ コマンドをサポートしている](the-wpdservicesampledriver-supporting-wpd-property-commands.md)トピック。

## <a name="span-idwpdobjectenumerationfindnextspanspan-idwpdobjectenumerationfindnextspanwpdobjectenumerationfindnext"></a><span id="WPD_OBJECT_ENUMERATION_FIND_NEXT"></span><span id="wpd_object_enumeration_find_next"></span>WPD\_オブジェクト\_列挙\_検索\_[次へ]


ドライバーの呼び出し、 **WpdObjectEnumerator::OnFindNext** WPD への応答ハンドラー\_コマンド\_オブジェクト\_列挙\_検索\_次のコマンドします。 ハンドラーが呼び出されます、 **FakeDevice::FindNext**メソッド、および、このメソッドを呼び出し、 **FakeContent::FindNext**メソッド。

次のコード例は、**派生**ハンドラーの呼び出し、 **FakeDevice::FindNext**メソッド。

```ManagedCPlusPlus
    if ((hr == S_OK) && (pEnumeratorContext != NULL))
    {
        hr = m_pDevice->FindNext(dwNumObjectsRequested, pEnumeratorContext, pObjectIDCollection, &dwNumObjectsEnumerated);
        CHECK_HR(hr, "Failed to get the next object");
    }
```

次のコード例は、 **FakeDevice::FindNext**メソッドの呼び出し、 **FakeContent::FindNext**メソッド。

```ManagedCPlusPlus
                    FakeContent* pChild = NULL;
                    if (pContent->FindNext(pEnumContext->m_Scope, dwStartIndex, &pChild))
                    {
                        hr = AddStringValueToPropVariantCollection(pObjectIDCollection, pChild->ObjectID);
                        CHECK_HR(hr, "Failed to add object [%ws]", pChild->ObjectID);

                        if (hr == S_OK)
                        {
                            // Update the number of children we are returning for this enumeration call
                            dwStartIndex++;
                            NumObjectsEnumerated++;
                        }
                    }
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





