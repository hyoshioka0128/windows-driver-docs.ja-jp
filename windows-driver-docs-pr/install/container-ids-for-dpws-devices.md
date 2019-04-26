---
title: DPWS デバイス用のコンテナー ID
description: DPWS デバイス用のコンテナー ID
ms.assetid: b613a25e-bedf-481c-8c86-9486af01b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9694d53ac64ea133009fb4c3f1aa4b88b50fb785
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346806"
---
# <a name="container-ids-for-dpws-devices"></a>DPWS デバイス用のコンテナー ID


Windows 7 以降、デバイスを PnP 拡張機能 (PNP-X) をサポートするデバイス プロファイルの Web サービス (DPWS) を含めることでコンテナー ID を指定できます、 **ContainerId**デバイスのメタデータ ドキュメント内の XML 要素。 DPWS とデバイスの DPWS メタデータ ドキュメントの詳細についてを参照してください、 [DPWS 仕様。](https://go.microsoft.com/fwlink/p/?linkid=142400)

**注**  以降 Windows 10 では、システムは、デバイスによって提供されたコンテナー ID を無視し、代わりに、独自のいずれかが生成されます。 これは、デバイスのエンドポイント参照のアドレス (EPR) またはデバイスの EPR (ない場合は、GUID) の sha-1 ハッシュから GUID を使用していずれか。

 

**ContainerId** XML 要素が次のように宣言されています。

```cpp
<df:ContainerId xmlns:df="">
  xs:string
</df:ContainerId>
```

**ContainerId** XML 要素の型が、値はグローバルに一意の識別子、文字列 (*GUID*) 書式設定します。 この文字列として書式設定 *{xxxxxxxx xxxx-xxxx-。}* します。

例を次に、 **ContainerId** XML 要素。

```cpp
<df:ContainerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:ContainerId>
```

&lt;ContainerId&gt; XML 要素が必要ですが、 &lt;ThisDevice&gt;デバイス メタデータ交換簡易オブジェクト アクセス プロトコル (SOAP) メッセージのセクション。 次の例では、適切な配置、 &lt;ContainerId&gt;メタデータ交換のメッセージ内の要素。

**注**  これは完全な DPWS メタデータ exchange ドキュメントではありません。 DPWS の詳細についてを参照してください、 [DPWS 仕様。](https://go.microsoft.com/fwlink/p/?linkid=142400)

 

```cpp
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wsdisco="http://schemas.xmlsoap.org/ws/2005/04/discovery"
    xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex"
    xmlns:wsd="http://schemas.xmlsoap.org/ws/2006/02/devprof"
    xmlns:df="http://schemas.microsoft.com/windows/2008/09/devicefoundation">

    <soap:Header>
        <!-- Place SOAP header information here.-->
    </soap:Header> 

    <soap:Body>
        <wsx:Metadata>

           <wsx:MetadataSection
                Dialect="http://schemas.xmlsoap.org/ws/2005/05/devprof/ThisModel">
                <wsd:ThisDevice>
                    <!-- Place ThisDevice metadata here.-->
                    <df:ContainerId>
                        <!--- Place the ContainerID GUID here.--->
                        {101392d0-5e91-11dd-ad8b-0800200c9a66}
                    </df:ContainerId>
                </wsd:ThisDevice>
            </wsx:MetadataSection>

        </wsx:Metadata>
    </soap:Body>
</soap:Envelope>
```

デバイスの DPWS メタデータ ドキュメントが含まれていない場合、 **ContainerId** 、プラグ アンド プレイ (PnP) マネージャーである XML 要素は、コンテナー ID とデバイスのエンドポイント参照のアドレスの値を使用

 

 





