---
title: デバイスの関係の取得
description: デバイスの関係の取得
ms.assetid: 2b0ead69-1fda-4024-a7c2-d6350060b5fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bccb6d4fe33f2543255ec7bb220c24732aabb58
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716858"
---
# <a name="retrieving-device-relations"></a>デバイスの関係の取得


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス リレーション プロパティ](https://docs.microsoft.com/previous-versions/ff541498(v=vs.85))します。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000、統一されたプロパティのモデルのプロパティのキーをサポートしても、これらのプロパティを表す対応するレジストリ エントリの値をサポートしています。 ただし、プラグ アンド プレイ (PnP) configuration manager の関数を呼び出すことによって、対応する情報を取得することができます。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポート デバイス関係のプロパティを取得する PnP 構成マネージャーの関数の呼び出し。 ただし、デバイスのリレーションシップのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルのプロパティのキーを使用する必要があります。

プロパティのキーを使用して、デバイス ドライバーのプロパティにアクセスする方法については、次を参照してください。[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)します。

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

        CM_GETIDLIST_FILTER_EJECTIONRELATIONS フラグを取得します[**取り出し関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_EjectionRelations** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-ejectionrelations) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

    -   CM_GETIDLIST_FILTER_REMOVALRELATIONS

        CM_GETIDLIST_FILTER_REMOVALRELATIONS フラグを取得します[**取り外し関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_RemovalRelations** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-removalrelations) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

    -   CM_GETIDLIST_FILTER_POWERRELATIONS

        CM_GETIDLIST_FILTER_POWERRELATIONS フラグ取得電源の関係によって提供される情報と同じですが、 [ **DEVPKEY_Device_PowerRelations** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-powerrelations) Windows Vista でのデバイス プロパティと以降のバージョン。

    -   CM_GETIDLIST_FILTER_BUSRELATIONS

        CM_GETIDLIST_FILTER_BUSRELATIONS フラグを取得します[**バス関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)、によって提供される情報と同じですが、 [ **DEVPKEY_Device_BusRelations**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-busrelations) Windows Vista およびそれ以降のバージョンでのデバイス プロパティ。

場合に呼び出し**CM_Get_Device_ID_List**成功すると、 **CM_Get_Device_ID_List**リレーションシップの要求された情報を取得し、CR_SUCCESS を返します。 それ以外の場合、 **CM_Get_Device_ID_List**プレフィックスで定義されている"CR_"でエラー コードのいずれかを返します*Cfgmgr32.h*します。

### <a href="" id="retrieving-the-parent-of-a-device-inst"></a> デバイス インスタンスの親を取得します。

Windows Server 2003、Windows XP、および Windows 2000 上の親デバイスのデバイスのインスタンス識別子を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)デバイス インスタンスの親のデバイスにデバイスのインスタンス ハンドルを取得します。

2.  呼び出す[ **CM_Get_Device_ID** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)以前の呼び出しによって取得された親デバイスにデバイスのインスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**cm _Get_Parent**します。

このプロシージャを使用して取得されたこの情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Parent プロパティによって表されるものと同じです。

### <a href="" id="retrieving-the-children-of-a-device-inst"></a>デバイス インスタンスの子を取得

Windows Server 2003、Windows XP、および Windows 2000 上のデバイス インスタンスの子デバイスのデバイスのインスタンス id を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Child** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_child)デバイス インスタンスに関連付けられている最初の子デバイスにデバイスのインスタンス ハンドルを取得します。

2.  呼び出す[ **CM_Get_Sibling** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_sibling)への呼び出しによって取得された最初の子デバイスのすべての兄弟のデバイスを列挙する必要がある回数**CM_Get_Child**します。

3.  呼び出す**CM_Get_Device_ID**への呼び出しによって返されたデバイス インスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**CM_Get_Child**と**CM_Get_兄弟**します。

このプロシージャを使用して取得されたこの情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Children プロパティによって表されるものと同じです。

### <a href="" id="retrieving-the-siblings-of-a-device-inst"></a>デバイス インスタンスの兄弟を取得します。

デバイス インスタンスでは、Windows Server 2003、Windows XP、および Windows 2000 Abc の兄弟のデバイスのデバイスのインスタンス id を取得するには、次の手順に従います。

1.  呼び出す、 [ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)デバイス インスタンスの親のデバイスにデバイスのインスタンス ハンドルを取得する関数を*Abc*します。

2.  呼び出す、 [ **CM_Get_Child** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_child)デバイス インスタンスの親のデバイスの最初の子デバイスにデバイスのインスタンス ハンドルを取得する関数を*Abc*します。

3.  呼び出す[ **CM_Get_Sibling** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_sibling)は、親デバイスの最初の子デバイスのすべての兄弟のデバイスを列挙するために必要な回数だけです。 この列挙体はデバイス インスタンスを識別するハンドルを返しますも*Abc*します。

4.  呼び出す[ **CM_Get_Device_ID** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)前の呼び出しによって返されたデバイス インスタンス ハンドルに関連付けられているデバイス インスタンス識別子を取得する**CM_Get_Sibling**. デバイス インスタンスへのハンドルを削除*Abc*親デバイスの最初の子デバイスの兄弟のデバイスの一覧から。

このプロシージャを使用して取得した情報は、Windows Vista およびそれ以降のバージョンの統一されたデバイス プロパティのモデルの DEVPKEY_Device_Siblings プロパティによって表されるものと同じです。 場合、 **cm _<em>Xxx</em>** が成功すると、このセクションで示す関数の呼び出し、 **cm _<em>Xxx</em>** 関数は、要求された情報を取得し、CR_SUCCESS を返します。 それ以外の場合、 **cm _<em>Xxx</em>** 関数は、プレフィックスで定義されている"CR_"でエラー コードのいずれかを返します*Cfgmgr32.h*します。

 

 





