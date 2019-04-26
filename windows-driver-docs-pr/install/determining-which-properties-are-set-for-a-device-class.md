---
title: デバイス クラスに設定するプロパティの決定
description: デバイス クラスに設定するプロパティの決定
ms.assetid: a8016b04-ae52-47d9-b3ef-74e0896aa825
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08fc5374cf0be9ccdf03a82dbcd69dde2793bfbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346178"
---
# <a name="determining-which-properties-are-set-for-a-device-class"></a>デバイス クラスに設定するプロパティの決定


次のトピックでは、Windows Vista 以降のバージョンの Windows でのデバイス クラスに対するクラス プロパティが設定を決定する方法について説明します。

[クラス プロパティがローカル コンピューター上のデバイス クラスに対する設定を決定します。](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc)

[リモート コンピューター上のデバイス クラスのどのクラス プロパティが設定を決定します。](#determining-which-class-properties-are-set-for-a-device-class-on-a-rem)

### <a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-loc"></a> クラス プロパティがローカル コンピューター上のデバイス クラスに対する設定を決定します。

ローカル コンピューター上のデバイス クラスのどのプロパティが設定を確認するのには、次の手順を実行します。

1.  呼び出す[ **SetupDiGetClassPropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551091)デバイス クラスの数のプロパティは設定を指定します。 次のパラメーター値を指定します。

    -   設定*ClassGuid*を識別する GUID へのポインター、[デバイス セットアップ クラス](device-setup-classes.md)または[デバイス インターフェイス クラス](device-interface-classes.md)クラス プロパティのキーの一覧を取得します。
    -   設定*PropertyKeyArray*に**NULL**します。
    -   設定*PropertyKeyCount*をゼロにします。
    -   設定*RequiredPropertyKeyCount* DWORD に型指定された変数へのポインター。
    -   デバイスのクラスが、デバイス セットアップ クラスの場合は、設定*フラグ*DICLASSPROP_INSTALLER。 それ以外の場合、デバイス クラスがデバイスのインターフェイス クラスの場合は、設定*フラグ*DICLASSPROP_INTERFACE にします。

    この最初の呼び出しに応答[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)、 **SetupDiGetClassPropertyKeys**設定\* *RequiredPropertyKeyCount*デバイス セットアップ クラスに設定されているプロパティの数、エラー コード、ERROR_INSUFFICIENT_BUFFER ログに記録し、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDevicePropertyKeys**もう一度と、次の変更を除き、最初の呼び出しで指定された同じパラメーターを指定します。
    -   設定*PropertyKeyArray*を[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-要求されたプロパティのキーの配列を受け取るバッファーへの型指定されたポインター。
    -   設定*PropertyKeyCount* DEVPROPKEY に型指定された値で、サイズの*PropertyKeyArray*バッファー。 最初の呼び出し**SetupDiGetClassPropertyKeys**の必要なサイズが返されます、 *PropertyKeyArray*内でバッファー \* *RequiredPropertyKeyCount*します。

場合は、2 つ目の呼び出し**SetupDiGetClassPropertyKeys**成功すると、関数は、要求されたプロパティのキーの配列を返し、 *PropertyKeyArray*バッファー、セット\* *RequiredPropertyKeyCount*バッファー、および返します内のプロパティのキーの数に**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetClassPropertyKeys**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

### <a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-rem"></a> リモート コンピューター上のデバイス クラスのどのクラス プロパティが設定を決定します。

リモート コンピューター上のデバイス クラスに設定されているクラスのプロパティを調べるに記載されている手順を実行[セットの決定をクラス プロパティがローカル コンピューター上のデバイス クラスに対する](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc)に次の変更:

-   呼び出す[ **SetupDiGetClassPropertyKeysEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551093)の代わりに[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)します。

-   両方に必要なパラメーター値を指定するだけでなく[ **SetupDiGetClassPropertyKeysEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551093)と[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)指定、 *MachineName* UNC 名を含む NULL で終わる文字列へのポインターに設定する必要があります、パラメーターなど、 \\ \\のコンピューターのプレフィックス。

 

 





