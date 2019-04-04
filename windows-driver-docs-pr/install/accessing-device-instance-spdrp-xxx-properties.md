---
title: デバイス インスタンス SPDRP_Xxx プロパティへのアクセス
description: デバイス インスタンス SPDRP_Xxx プロパティへのアクセス
ms.assetid: 15ee51f8-1904-43ee-8bc2-311688c860e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f502ed9ae1bd56d222bd9a36cbe33826598203f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572893"
---
# <a name="accessing-device-instance-spdrpxxx-properties"></a>デバイス インスタンス SPDRP_Xxx プロパティへのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)で定義されている SPDRP_Xxx 識別子に対応するデバイスのインスタンスのプロパティをサポートしている*Setupapi.h*. これらのプロパティには、デバイスのインスタンスの構成が特徴付けられます。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。 Windows Server 2003、Windows XP、および Windows 2000 は、これらのデバイス ドライバーのプロパティもサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 以前の Windows バージョンが、SPDRP_ を使用する代わりに、*Xxx*インスタンスのプロパティの識別子を表し、デバイスにアクセスします。

維持するために、デバイス インスタンス プロパティにアクセスする SPDRP_Xxx 識別子を使用してを以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性もサポートします。 ただし、Windows Vista および Windows の以降のバージョンでこれらのプロパティへのアクセスに対応するプロパティのキーを使用する必要があります。

SPDRP_Xxx 識別子が対応するデバイスのシステム定義のインスタンスのプロパティの一覧は、[デバイス プロパティをある対応する SPDRP_Xxx 識別子](https://msdn.microsoft.com/library/windows/hardware/ff541469)を参照してください。 デバイス インスタンスのプロパティは、Windows Vista 以降のバージョンの Windows でのプロパティにアクセスするために使用するプロパティのキーを一覧表示されます。 各プロパティはキーに対応する SPDRP_ が含まれる示される情報*Xxx* Windows Server 2003、Windows XP、および Windows 2000 のプロパティへのアクセスに使用できる識別子。

プロパティのキーを使用して、Windows Vista および以降のバージョンの Windows デバイスのインスタンスのプロパティにアクセスする方法については、[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)を参照してください。

### <a name="accessing-a-device-property"></a>デバイスのプロパティにアクセスします。

プロパティにアクセスするデバイスのインスタンス、SPDRP_ に対応する*Xxx*で Windows Server 2003、Windows XP、および Windows 2000 では、識別子は、次の SetupAPI 関数を使用します。

-   [**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

    この関数は、SPDRP_ で指定されているデバイス プロパティを取得*Xxx*識別子。

-   [**SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)

    この関数は、SPDRP_ で指定されているデバイスのプロパティを設定*Xxx*識別子。

### <a name="retrieving-a-device-property"></a>デバイスのプロパティを取得します。

Windows Server 2003、Windows XP、および Microsoft Windows 2000 でのデバイス プロパティを取得するには、次の手順に従います。

1.  呼び出す**SetupDiGetDeviceRegistryProperty**プロパティの値のバイト単位のサイズを取得します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*に要求されたプロパティ値を取得する対象のデバイスのインスタンスを含むデバイス情報のセットを識別するハンドル。
    -   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)要求されたプロパティ値を取得する対象のデバイスのインスタンスを表す構造体です。
    -   設定*プロパティ*、SPDRP_ に*Xxx*識別子。 これらの識別子と、対応するデバイスのプロパティの説明の一覧は、の説明を参照して、*プロパティ*パラメーターに含まれている[ **SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169).
    -   設定*PropertyRegDataType* DWORD に型指定された変数へのポインター。
    -   設定*PropertyBuffer*に**NULL**します。
    -   設定*PropertyBufferSize*をゼロにします。
    -   設定*RequiredSize*を受け取る、サイズ、プロパティ値のバイトで DWORD に型指定された変数へのポインター。

    呼び出しに応答[ **SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)、 **SetupDiGetDeviceRegistryProperty**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDeviceRegistryProperty**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。

    -   設定*PropertyBuffer*を要求されたプロパティ値を受け取るバイトに型指定されたバッファーへのポインター。
    -   設定*PropertyBufferSize*サイズ (バイト単位) の*PropertyBuffer*バッファー。 最初の呼び出し**SetupDiGetDeviceRegistryProperty** PropertyBuffer バッファーの必要なサイズを取得した\* *RequiredSize*します。

    2 番目の呼び出しに場合**SetupDiGetDeviceRegistryProperty**成功すると、 **SetupDiGetDeviceRegistryProperty**設定\* *PropertyRegDataType*に、プロパティの値のレジストリ データ型の設定、 *PropertyBuffer* 、プロパティの値を設定するバッファー \* *RequiredSize*サイズ (バイト単位) のプロパティの値でした取得し、返します**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceRegistryProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

### <a name="setting-a-device-property"></a>デバイス プロパティの設定

Windows Server 2003、Windows XP、および Windows 2000 では、デバイス プロパティを設定するには、呼び出す[ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169)し、次のパラメーター値を指定します。

-   設定*DeviceInfoSet*プロパティの値を設定する対象のデバイスのインスタンスを含むデバイス情報のセットへのハンドル。

-   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)プロパティの値を設定する対象のデバイスのインスタンスを表す構造体です。

-   設定*プロパティ*、SPDRP_ に*Xxx*識別子。

-   設定*PropertyBuffer*プロパティの値を格納するバイトに型指定されたバッファーへのポインター。

-   設定*PropertyBufferSize*サイズ (バイト単位) のプロパティの値をで指定されている、 *PropertyBuffer*バッファー。

この呼び出し場合**SetupDiSetDeviceRegistryProperty**成功すると、 **SetupDiSetDeviceRegistryProperty**デバイス インスタンスのプロパティを設定し、返します**TRUE**。 関数呼び出しが失敗した場合、 **SetupDiSetDeviceRegistryProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





