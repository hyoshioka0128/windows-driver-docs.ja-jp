---
title: インターフェイス ハンドラー プラグイン
description: インターフェイス ハンドラー プラグイン
ms.assetid: cd81f622-d11c-4b40-ac78-9324716e0a2c
keywords:
- カーネルストリーミングプロキシ WDK AVStream、インターフェイスハンドラー
- インターフェイスハンドラーの WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d90c270d907888764e36e4d9787c421e88878ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845565"
---
# <a name="interface-handler-plug-in"></a>インターフェイス ハンドラー プラグイン


インターフェイスハンドラープラグインを記述して、KS ミニドライバーによって公開されているドライバー固有のプロパティセットにプログラムでユーザーモードでアクセスできるようにすることができます。 まず、「 [KS プロキシプラグインの登録](registering-ks-proxy-plug-ins.md)」の説明に従ってオブジェクトを登録します。

インターフェイスプラグインクラスを[Cunknown](https://go.microsoft.com/fwlink/p/?linkid=106451)から派生させることができます。

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

インターフェイスプラグインは、作成時に MS が提供する KS プロキシで集計される、ベンダーが提供する COM インターフェイスです。

具体的には、プラグインの**CreateInstance**メソッドは KS プロキシへのポインターを外部不明として受け取ります。

次に、この外部オブジェクトに対して、MS 提供の[IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nn-dsound-ikspropertyset)インターフェイスへのポインターを照会できます。

```cpp
hResult = piOuterUnknown->QueryInterface(
                __uuidof( piKsPropertySet ),
                 &piKsPropertySet );
```

次に、 **CreateInstance**からインターフェイスのコンストラクターを呼び出して、インターフェイスハンドラーオブジェクトのインスタンスを作成します。

コンストラクターの呼び出しで、 **IKsPropertySet**へのポインターをパラメーターとして指定します。 コンストラクターは、iKsPropertySet へのポインターを、前の宣言の m\_piKsPropertySet メンバーとして保持します。

これで、 [**IKsPropertySet:: get**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikspropertyset-get)と[**IKsPropertySet:: Set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nf-dsound-ikspropertyset-set)を呼び出して、ドライバーによって公開されるプロパティを操作するクラスに get メソッドと set メソッドを実装できるようになりました。

または、 **IKsObject**インターフェイスへのポインターの外側の unknown に対してクエリを実行することもできます。 次に、 [**IKsObject:: KsGetObjectHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-iksobject-ksgetobjecthandle)を呼び出してファイルハンドルを取得します。 ここで、このファイルハンドルを使用して[**KsSynchronousIoControlDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kssynchronousiocontroldevice)を呼び出すことによってデバイスのプロパティを操作します。

 

 




