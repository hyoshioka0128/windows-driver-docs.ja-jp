---
title: DXGKMDT\_OPM\_コネクタ\_種類の列挙型
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 57A2F351-99F1-425A-99E3-1167CEFF9FDD
keywords:
- DXGKMDT_OPM_CONNECTOR_TYPE 列挙ディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKMDT_OPM_CONNECTOR_TYPE
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c7e1f6caf9e6ec2066887a4c71b05a1077857df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579901"
---
# <a name="dxgkmdtopmconnectortype-enumeration"></a>DXGKMDT\_OPM\_コネクタ\_種類の列挙型


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _DXGKMDT_OPM_CONNECTOR_TYPE {
  DXGKMDT_OPM_CONNECTOR_TYPE_OTHER                     = -1,
  DXGKMDT_OPM_CONNECTOR_TYPE_HD15                      = 0,
  DXGKMDT_OPM_CONNECTOR_TYPE_SVIDEO                    = 1,
  DXGKMDT_OPM_CONNECTOR_TYPE_COMPOSITE_VIDEO           = 2,
  DXGKMDT_OPM_CONNECTOR_TYPE_COMPONENT_VIDEO           = 3,
  DXGKMDT_OPM_CONNECTOR_TYPE_DVI                       = 4,
  DXGKMDT_OPM_CONNECTOR_TYPE_HDMI                      = 5,
  DXGKMDT_OPM_CONNECTOR_TYPE_LVDS                      = 6,
  DXGKMDT_OPM_CONNECTOR_TYPE_D_JPN                     = 8,
  DXGKMDT_OPM_CONNECTOR_TYPE_SDI                       = 9,
  DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EXTERNAL      = 10,
  DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EMBEDDED      = 11,
  DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EXTERNAL              = 12,
  DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EMBEDDED              = 13,
  DXGKMDT_OPM_CONNECTOR_TYPE_RESERVED                  = 14,
  DXGKMDT_OPM_CONNECTOR_TYPE_MIRACAST                  = 15,
  DXGKMDT_OPM_COPP_COMPATIBLE_CONNECTOR_TYPE_INTERNAL  = 0x80000000
} DXGKMDT_OPM_CONNECTOR_TYPE;
```

<a name="constants"></a>定数
---------

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_OTHER"></span><span id="dxgkmdt_opm_connector_type_other"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_OTHER**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_HD15"></span><span id="dxgkmdt_opm_connector_type_hd15"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_HD15**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_SVIDEO"></span><span id="dxgkmdt_opm_connector_type_svideo"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_SVIDEO**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_COMPOSITE_VIDEO"></span><span id="dxgkmdt_opm_connector_type_composite_video"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_COMPOSITE\_VIDEO**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_COMPONENT_VIDEO"></span><span id="dxgkmdt_opm_connector_type_component_video"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_COMPONENT\_VIDEO**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DVI"></span><span id="dxgkmdt_opm_connector_type_dvi"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_DVI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_HDMI"></span><span id="dxgkmdt_opm_connector_type_hdmi"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_HDMI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_LVDS"></span><span id="dxgkmdt_opm_connector_type_lvds"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_LVDS**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_D_JPN"></span><span id="dxgkmdt_opm_connector_type_d_jpn"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_D\_JPN**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_SDI"></span><span id="dxgkmdt_opm_connector_type_sdi"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_SDI**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EXTERNAL"></span><span id="dxgkmdt_opm_connector_type_displayport_external"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_DISPLAYPORT\_EXTERNAL**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_DISPLAYPORT_EMBEDDED"></span><span id="dxgkmdt_opm_connector_type_displayport_embedded"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_DISPLAYPORT\_EMBEDDED**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EXTERNAL"></span><span id="dxgkmdt_opm_connector_type_udi_external"></span>**DXGKMDT\_OPM\_コネクタ\_型\_UDI\_外部**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_UDI_EMBEDDED"></span><span id="dxgkmdt_opm_connector_type_udi_embedded"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_UDI\_EMBEDDED**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_RESERVED"></span><span id="dxgkmdt_opm_connector_type_reserved"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_RESERVED**

<span id="DXGKMDT_OPM_CONNECTOR_TYPE_MIRACAST"></span><span id="dxgkmdt_opm_connector_type_miracast"></span>**DXGKMDT\_OPM\_CONNECTOR\_TYPE\_MIRACAST**

<span id="DXGKMDT_OPM_COPP_COMPATIBLE_CONNECTOR_TYPE_INTERNAL"></span><span id="dxgkmdt_opm_copp_compatible_connector_type_internal"></span>**DXGKMDT\_OPM\_COPP\_COMPATIBLE\_CONNECTOR\_TYPE\_INTERNAL**

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmdt.h (D3dkmdt.h を含む)</td>
</tr>
</tbody>
</table>

 

 





