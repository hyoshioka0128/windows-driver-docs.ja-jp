---
Description: Support for enumeration commands (WpdBasicHardwareDriverSample)
title: 列挙型のコマンド (WpdBasicHardwareDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 655b946704ff169cc07113ad307f9de6e3b6d51d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528278"
---
# <a name="support-for-enumeration-commands-wpdbasichardwaredriversample"></a>列挙型のコマンド (WpdBasicHardwareDriverSample) のサポート


ドライバーのサンプルでは、列挙体の 3 つのコマンドをサポートします。 これらのコマンドが最初に、処理、 **WpdObjectEnumerator::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、すべてで、 *WpdObjectEnum.cpp*ファイル。

次の表の情報は、ことを示していますの各プロパティがサポートされているコマンドのハンドラーの名前と共に、 **DispatchMessage**特定のコマンドを処理するときに呼び出します。 これらのコマンドが発行されるは、アプリケーションがいくつかのメソッドのいずれかを呼び出すときに、 **IPortableDeviceContent**または**IEnumPortableDeviceObjectIDs**インターフェイス。

| コマンド                                        | ハンドラー     | 説明                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD\_コマンド\_オブジェクト\_列挙\_開始\_検索 | OnStartFind | 新しい列挙体の内容を作成し、クライアントのコンテキスト マップに格納します。 |
| WPD\_コマンド\_オブジェクト\_列挙\_検索\_[次へ]  | 派生  | 要求されたオブジェクトのオブジェクト識別子を返します。                     |
| WPD\_コマンド\_オブジェクト\_列挙\_エンド\_検索   | OnEndFind   | 列挙の終了時に必要なクリーンアップを実行します。            |

 

サンプル ドライバーのコードは、そのまま、WPD の\_コマンド\_オブジェクト\_列挙\_検索\_次へと WPD\_コマンド\_オブジェクト\_列挙体\_エンド\_検索ハンドラー。 WPD のコードの部分が変更された、\_コマンド\_オブジェクト\_列挙\_開始\_検索ハンドラー。

## <a name="span-idwpdcommandobjectenumerationstartfindspanspan-idwpdcommandobjectenumerationstartfindspanwpdcommandobjectenumerationstartfind"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD\_COMMAND\_OBJECT\_ENUMERATION\_START\_FIND


ドライバーの呼び出し、 **WpdObjectEnumerator::OnStartFind** WPD への応答ハンドラー\_コマンド\_オブジェクト\_列挙\_開始\_検索コマンド。 ハンドラーがさらに、作成、初期化、およびクライアント コンテキスト マップに新しい列挙体の内容を追加します。 サンプル ドライバーの場合、 **InitializeEnumerationContext**内から呼び出されるヘルパー関数、 **OnStartFind**ハンドラーが変更されました。

両方に、変更、 **OnStartFind**ハンドラーと**InitializeEnumerationContext**ヘルパー関数がサポートされなくなったオブジェクトのサポートは削除し (記憶域、フォルダー、ファイル オブジェクト) とセンサーのオブジェクトのサポートを追加します。 コードを次に、 **InitalizeEnumerationContext**ヘルパー関数。

```cpp
VOID WpdObjectEnumerator::InitializeEnumerationContext(
    WpdObjectEnumeratorContext* pEnumeratorContext,
    CAtlStringW                 strParentObjectID)
{
    if (pEnumeratorContext == NULL)
    {
        return;
    }

    // Initialize the enumeration context with the parent object identifier
    pEnumeratorContext->m_strParentObjectID = strParentObjectID;

    // Our sample driver has a very simple object structure where we know
    // how many children are under each parent.
    // The eumeration context is initialized below with this information.
    if (strParentObjectID.CompareNoCase(L"") == 0)
    {
        // Clients passing an &#39;empty&#39; string for the parent are asking for the
        // &#39;DEVICE&#39; object.  We should return 1 child in this case.
        pEnumeratorContext->m_TotalChildren = 1;
    }
    else if (strParentObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
    {
        // The device object contains 1 child (the sensor object).
        pEnumeratorContext->m_TotalChildren = 1;
    }
    // If the sensor objects have children, add them here...
    else 
    {
        // The sensor object contains 0 children.
        pEnumeratorContext->m_TotalChildren = 0;
    }
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





