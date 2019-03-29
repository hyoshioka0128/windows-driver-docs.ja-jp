---
title: SPCRP_Xxx プロパティの取得
description: SPCRP_Xxx プロパティの取得
ms.assetid: a5d52da9-a593-42bd-aeaf-8ab203bc3d21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94ea84c139cfaec7a800734a67c3dcd632376ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572757"
---
# <a name="retrieving-spcrpxxx-properties"></a>SPCRP_Xxx プロパティの取得


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)で定義されている SPCRP_Xxx 識別子に対応するデバイスのインスタンスのプロパティをサポートしている*Setupapi.h*. これらのプロパティ特性を表す、[デバイス セットアップ クラス](device-setup-classes.md)します。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 もこれらのデバイス セットアップ クラスのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows バージョンを使用して、SPCRP_*Xxx*識別子を表すし、デバイスへのアクセスをクラスのプロパティを設定します。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンも使用をサポートして SPCRP_*Xxx*デバイスのセットアップへのアクセスに識別子クラスのプロパティ。 ただし、デバイス セットアップ クラスのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルのプロパティのキーを使用する必要があります。

システム定義のデバイス セットアップ クラスのプロパティの一覧は、次を参照してください。[デバイス セットアップ クラスのプロパティに対応している SPCRP_Xxx 識別子](https://msdn.microsoft.com/library/windows/hardware/ff542245)します。 デバイス セットアップ クラスのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子が表示されます。 プロパティのキーで提供される情報は、対応する SPCRP_ も含まれています。*Xxx*プロパティを、Windows Server 2003、Windows XP、および Windows 2000 へのアクセスに使用できる識別子。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、次を参照してください。[にアクセスするデバイス クラスのプロパティ (Windows Vista 以降)](accessing-device-class-properties--windows-vista-and-later-.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス セットアップ クラスのプロパティを取得する、 [ **SetupDiGetClassRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551097)関数。

SetupDiGetClassRegistryProperty を使用して、SPCRP_Xxx 識別子に対応するプロパティを取得する、次の手順に従います。

1.  呼び出す**SetupDiGetClassRegistryProperty**し、次のパラメーター値を指定します。

    -   設定*ClassGuid*プロパティを取得する対象のデバイス セットアップ クラスを表す GUID へのポインター。
    -   設定*プロパティ*"SPCRP_"プレフィックスを持つプロパティの識別子をプロパティ値のサイズを取得します。
    -   設定*PropertyRegDataType*に**NULL**します。
    -   設定*PropertyBuffer*に**NULL**します。
    -   設定*PropertyBufferSize*をゼロにします。
    -   設定*RequiredSize*を要求されたプロパティのバイト単位のサイズを受け取る DWORD に型指定された変数へのポインター。
    -   設定*MachineName*コンピューターの名前にします。
    -   設定するために予約**NULL**します。

    呼び出しに応答[ **SetupDiGetClassRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551097)、 **SetupDiGetClassRegistryProperty**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetClassRegistryProperty**プロパティ値を取得し、次の変更を除き、最初の呼び出しで指定された同じパラメーターを指定します。
    -   設定*PropertyBuffer*プロパティの値を受け取るバッファーへのポインター。
    -   設定*PropertyBufferSize*サイズ (バイト単位) の*PropertyBuffer*バッファー。 最初の呼び出し**SetupDiGetClassRegistryProperty**の必要なサイズを取得、 *PropertyBuffer*内でバッファー \* *RequiredSize*します。

2 番目の呼び出しに場合**SetupDiGetClassRegistryProperty**成功すると、 **SetupDiGetClassRegistryProperty**設定\* *PropertyRegDataType*に、レジストリ データ型では、設定、 *PropertyBuffer* 、プロパティの値を設定するバッファー \* *PropertyBufferSize*プロパティ値、および返しますのバイト単位のサイズ**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetClassRegistryProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





