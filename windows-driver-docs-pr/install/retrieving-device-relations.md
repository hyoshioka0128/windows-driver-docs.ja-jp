---
title: デバイスの関係を取得します。
description: デバイスの関係を取得します。
ms.assetid: 2b0ead69-1fda-4024-a7c2-d6350060b5fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f51fbb5d270610e2cbc83ffcdfb36e8ac788de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536723"
---
# <a name="retrieving-device-relations"></a>デバイスの関係を取得します。


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス リレーション プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541498)します。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000、統一されたプロパティのモデルのプロパティのキーをサポートしても、これらのプロパティを表す対応するレジストリ エントリの値をサポートしています。 ただし、プラグ アンド プレイ (PnP) configuration manager の関数を呼び出すことによって、対応する情報を取得することができます。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポート デバイス関係のプロパティを取得する PnP 構成マネージャーの関数の呼び出し。 ただし、デバイスのリレーションシップのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルのプロパティのキーを使用する必要があります。

プロパティのキーを使用して、デバイス ドライバーのプロパティにアクセスする方法については、[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)を参照してください。

Windows Server 2003、Windows XP、および Windows 2000 でデバイスの関係のプロパティにアクセスする方法については、次のトピックを参照してください。

[取り出し関係、リレーションの削除、および電源関係、およびバスのリレーションを取得します。](#retrieving-ejection-relations--removal-relations--and-power-relations-)

[デバイス インスタンスの親を取得します。](#retrieving-the-parent-of-a-device-inst)

[デバイス インスタンスの子を取得](#retrieving-the-children-of-a-device-inst)

[デバイス インスタンスの兄弟を取得します。](#retrieving-the-siblings-of-a-device-inst)

### <a href="" id="retrieving-ejection-relations--removal-relations--and-power-relations-"></a> 取り出し関係、リレーションの削除、および電源関係、およびバスのリレーションを取得します。

Windows Server 2003、Windows XP、および Windows 2000 のデバイスの関係情報を取得する**CM_Get_Device_ID_List**し、次のパラメーター値を指定します。

-   設定*pszFilter*リレーション情報を取得する対象のデバイスのインスタンス識別子を指定する NULL で終わる文字列へのポインター。

-   設定*バッファー*を NULL で終わるデバイス インスタンス識別子の一覧を受け取るバッファーへのポインター。 一覧については、追加の NULL 文字で終了します。 必要なバッファー サイズを取得するにはで、 **CM_Get_Device_ID_List_Size**関数。

-   設定*BufferLen*文字数、サイズの*バッファー*バッファー。

-   設定*ulFlags*リレーションに対応する情報を取得する次のフラグのいずれかに。
    -   CM_GETIDLIST_FILTER_EJECTIONRELATIONS

        CM_GETIDLIST_FILTER_EJECTIONRELATIONS フラグを取得します[**取り出し関係**](https://msdn.microsoft.com/library/windows/hardware/ff551670)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_EjectionRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542482) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

    -   CM_GETIDLIST_FILTER_REMOVALRELATIONS

        CM_GETIDLIST_FILTER_REMOVALRELATIONS フラグを取得します[**取り外し関係**](https://msdn.microsoft.com/library/windows/hardware/ff551670)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_RemovalRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542614) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

    -   CM_GETIDLIST_FILTER_POWERRELATIONS

        CM_GETIDLIST_FILTER_POWERRELATIONS フラグ取得電源の関係によって提供される情報と同じですが、 [ **DEVPKEY_Device_PowerRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542588) Windows Vista でのデバイス プロパティと以降のバージョン。

    -   CM_GETIDLIST_FILTER_BUSRELATIONS

        CM_GETIDLIST_FILTER_BUSRELATIONS フラグを取得します[**バス関係**](https://msdn.microsoft.com/library/windows/hardware/ff551670)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_BusRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542368) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

場合に呼び出し**CM_Get_Device_ID_List**成功すると、 **CM_Get_Device_ID_List**リレーションシップの要求された情報を取得し、CR_SUCCESS を返します。 それ以外の場合、 **CM_Get_Device_ID_List**プレフィックスで定義されている"CR_"でエラー コードのいずれかを返します*Cfgmgr32.h*します。

### <a href="" id="retrieving-the-parent-of-a-device-inst"></a> デバイス インスタンスの親を取得します。

Windows Server 2003、Windows XP、および Windows 2000 上の親デバイスのデバイスのインスタンス識別子を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)デバイス インスタンスの親のデバイスにデバイスのインスタンス ハンドルを取得します。

2.  呼び出す[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)以前の呼び出しによって取得された親デバイスにデバイスのインスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**cm _Get_Parent**します。

このプロシージャを使用して取得されたこの情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Parent プロパティによって表されるものと同じです。

### <a href="" id="retrieving-the-children-of-a-device-inst"></a>デバイス インスタンスの子を取得

Windows Server 2003、Windows XP、および Windows 2000 上のデバイス インスタンスの子デバイスのデバイスのインスタンス id を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Child** ](https://msdn.microsoft.com/library/windows/hardware/ff538074)デバイス インスタンスに関連付けられている最初の子デバイスにデバイスのインスタンス ハンドルを取得します。

2.  呼び出す[ **CM_Get_Sibling** ](https://msdn.microsoft.com/library/windows/hardware/ff538674)への呼び出しによって取得された最初の子デバイスのすべての兄弟のデバイスを列挙する必要がある回数**CM_Get_Child**します。

3.  呼び出す**CM_Get_Device_ID**への呼び出しによって返されたデバイス インスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**CM_Get_Child**と**CM_Get_兄弟**します。

このプロシージャを使用して取得されたこの情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Children プロパティによって表されるものと同じです。

### <a href="" id="retrieving-the-siblings-of-a-device-inst"></a>デバイス インスタンスの兄弟を取得します。

デバイス インスタンスでは、Windows Server 2003、Windows XP、および Windows 2000 Abc の兄弟のデバイスのデバイスのインスタンス id を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)デバイス インスタンスの親のデバイスにデバイスのインスタンス ハンドルを取得する関数を*Abc*します。

2.  呼び出す、 [ **CM_Get_Child** ](https://msdn.microsoft.com/library/windows/hardware/ff538074)デバイス インスタンスの親のデバイスの最初の子デバイスにデバイスのインスタンス ハンドルを取得する関数を*Abc*します。

3.  呼び出す[ **CM_Get_Sibling** ](https://msdn.microsoft.com/library/windows/hardware/ff538674)は、親デバイスの最初の子デバイスのすべての兄弟のデバイスを列挙するために必要な回数だけです。 この列挙体はデバイス インスタンスを識別するハンドルを返しますも*Abc*します。

4.  呼び出す[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)前の呼び出しによって返されたデバイス インスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**CM_Get_Sibling**. デバイス インスタンスへのハンドルを削除*Abc*親デバイスの最初の子デバイスの兄弟のデバイスの一覧から。

このプロシージャを使用して取得した情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Siblings プロパティによって表されるものと同じです。 場合、 **cm _ * Xxx*** このセクションで示す関数の呼び出しが成功すると、 **cm _ * Xxx*** 関数は、要求された情報を取得し、CR_SUCCESS を返します。 それ以外の場合、 **cm _ * Xxx*** プレフィックスで定義されている"CR_"でエラー コードのいずれかを返します*Cfgmgr32.h*します。

 

 





