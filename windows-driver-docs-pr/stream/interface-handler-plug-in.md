---
title: インターフェイス ハンドラー プラグイン
description: インターフェイス ハンドラー プラグイン
ms.assetid: cd81f622-d11c-4b40-ac78-9324716e0a2c
keywords:
- カーネル ストリーミング プロキシ WDK AVStream、ハンドラーのインターフェイス
- インターフェイス ハンドラー WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d84fba54f75adecaa81bab881d8790e3a63c377
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370915"
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

この MS 標準へのポインターの外側のオブジェクトをクエリできる[IKsPropertySet](https://msdn.microsoft.com/library/windows/hardware/ff560718)インターフェイス。

```cpp
hResult = piOuterUnknown->QueryInterface(
                __uuidof( piKsPropertySet ),
                 &piKsPropertySet );
```

その後から**CreateInstance**、インターフェイス ハンドラー オブジェクトのインスタンスを作成するインターフェイスのコンス トラクターを呼び出します。

ポインターを提供**IKsPropertySet**コンス トラクターの呼び出しでパラメーターとして。 コンス トラクターは、m と iKsPropertySet へのポインターを保持し\_piKsPropertySet メンバーで、前の宣言。

これで Get を実装し、クラスのメソッドを設定できます呼び出す[ **IKsPropertySet::Get** ](https://msdn.microsoft.com/library/windows/hardware/ff560719)と[ **IKsPropertySet::Set** ](https://msdn.microsoft.com/library/windows/hardware/ff560721)プロパティは、ドライバーによって公開されている操作それぞれに。

ポインターの不明な外部のクエリを実行する代わりに、その**IKsObject**インターフェイス。 呼び出して[ **IKsObject::KsGetObjectHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff559890)ファイル ハンドルを取得します。 呼び出してデバイスのプロパティを操作するようになりました[ **KsSynchronousIoControlDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff567143)をこのファイルのハンドル。

 

 




