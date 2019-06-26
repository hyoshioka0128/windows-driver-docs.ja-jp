---
title: インターフェイス ハンドラー プラグイン
description: インターフェイス ハンドラー プラグイン
ms.assetid: cd81f622-d11c-4b40-ac78-9324716e0a2c
keywords:
- カーネル ストリーミング プロキシ WDK AVStream、ハンドラーのインターフェイス
- インターフェイス ハンドラー WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11c5e3759b86c4098d042f3e5037d5a277e1496a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360658"
---
# <a name="interface-handler-plug-in"></a>インターフェイス ハンドラー プラグイン


KS ミニドライバーによって公開されるドライバー固有のプロパティ セットへのユーザー モードのプログラムによるアクセスを提供するプラグイン インターフェイス ハンドラーを記述することができます。 」の説明に従って、オブジェクトを最初に、登録[KS プロキシの登録にプラグイン](registering-ks-proxy-plug-ins.md)します。

派生させることが、インターフェイスのプラグイン クラス[CUnknown](https://go.microsoft.com/fwlink/p/?linkid=106451):

```cpp
class CMyPluginInterface : public CUnknown 
{
public:
    // creation method
    static CUnknown* CALLBACK CreateInstance( LPUNKNOWN piOuterUnknown, HRESULT* phResult );
private:
 CMyPluginInterface( IKsPropertySet* piKsPropertySet );
    IKsPropertySet* m_piKsPropertySet;
};
```

プラグインのインターフェイスは、ベンダーから提供された COM インターフェイスで MS が提供 KS プロキシによる集計の作成時です。

具体的には、 **CreateInstance**プラグインのメソッドが不明な外部として KS プロキシへのポインターを受け取ります。

この MS 標準へのポインターの外側のオブジェクトをクエリできる[IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nn-dsound-ikspropertyset)インターフェイス。

```cpp
hResult = piOuterUnknown->QueryInterface(
                __uuidof( piKsPropertySet ),
                 &piKsPropertySet );
```

その後から**CreateInstance**、インターフェイス ハンドラー オブジェクトのインスタンスを作成するインターフェイスのコンス トラクターを呼び出します。

ポインターを提供**IKsPropertySet**コンス トラクターの呼び出しでパラメーターとして。 コンス トラクターは、m と iKsPropertySet へのポインターを保持し\_piKsPropertySet メンバーで、前の宣言。

これで Get を実装し、クラスのメソッドを設定できます呼び出す[ **IKsPropertySet::Get** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikspropertyset-get)と[ **IKsPropertySet::Set** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nf-dsound-ikspropertyset-set)プロパティは、ドライバーによって公開されている操作それぞれに。

ポインターの不明な外部のクエリを実行する代わりに、その**IKsObject**インターフェイス。 呼び出して[ **IKsObject::KsGetObjectHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-iksobject-ksgetobjecthandle)ファイル ハンドルを取得します。 呼び出してデバイスのプロパティを操作するようになりました[ **KsSynchronousIoControlDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kssynchronousiocontroldevice)をこのファイルのハンドル。

 

 




