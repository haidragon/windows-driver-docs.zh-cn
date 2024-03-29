---
title: 音频驱动程序结构
description: 音频驱动程序结构
ms.assetid: 8257342f-474a-42b3-809d-96fdeede398b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ae243af6e5d5088f3a8e46579b2e0f38bb885e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355722"
---
# <a name="audio-drivers-structures"></a>音频驱动程序结构

## <span id="ddk_audio_drivers_structures_ks"></span><span id="DDK_AUDIO_DRIVERS_STRUCTURES_KS"></span>

本部分介绍使用 WDM 音频微型端口驱动程序的结构。 结构的列表如下所示：

[**APO\_REG\_属性**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apo_reg_properties)

[**APOInitBaseStruct**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitbasestruct)

[**APOInitSystemEffects**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects)

[**APOInitSystemEffects2**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects2)

[**AudioFXExtensionParams**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-audiofxextensionparams)

[**DMUS\_KERNEL\_EVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)

[**DRMFORWARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-tagdrmforward)

[**DRMRIGHTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-tagdrmrights)

[**DS3DVECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ds3dvector)

[**KSAC3\_ALTERNATE\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_alternate_audio)

[**KSAC3\_BIT\_STREAM\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)

[**KSAC3\_DIALOGUE\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_dialogue_level)

[**KSAC3\_DOWNMIX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_downmix)

[**KSAC3\_错误\_隐蔽**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_error_concealment)

[**KSAC3\_语言\_代码**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537081(v=vs.85))

[**KSAC3\_ROOM\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_room_type)

[**KSAUDIO\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSAUDIO\_COPY\_PROTECTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection)

[**KSAUDIO\_DYNAMIC\_RANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

[**KSAUDIO\_MIC\_ARRAY\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSAUDIO\_麦克风\_协调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_microphone_coordinates)

[**KSAUDIO\_MIX\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mix_caps)

[**KSAUDIO\_MIXCAP\_TABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSAUDIO\_MIXLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSAUDIO\_PACKETSIZE\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)

[**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

[**KSAUDIO\_POSITION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position)

[**KSAUDIO\_POSITIONEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSAUDIO\_PREFERRED\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_preferred_status)

[**KSAUDIO\_PRESENTATION\_POSITION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_presentation_position)

[**KSAUDIOENGINE\_缓冲区\_大小\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSAUDIOENGINE\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor)

[**KSAUDIOENGINE\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSDATARANGE\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)

[**KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_music)

[**KSDRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-ksdrmaudiostream_contentid)

[**KSDSOUND\_BUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdsound_bufferdesc)

[**KSDS3D\_BUFFER\_ALL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_buffer_all)

[**KSDS3D\_BUFFER\_CONE\_ANGLES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

[**KSDS3D\_HRTF\_INIT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)

[**KSDS3D\_HRTF\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)

[**KSDS3D\_ITD\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_itd_params)

[**KSDS3D\_ITD\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_itd_params_msg)

[**KSDS3D\_LISTENER\_ALL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_listener_all)

[**KSDS3D\_LISTENER\_ORIENTATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_listener_orientation)

[**KSJACK\_说明**](ksjack-description.md)

[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[**KSJACK\_接收器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksjack_sink_information)

[**KSMUSICFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksmusicformat)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSP\_DRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-ksp_drmaudiostream_contentid)

[**KSP\_PINMODE**](https://docs.microsoft.com/windows/desktop/api/msapofxproxy/ns-msapofxproxy-tagksp_pinmode)

[KSRTAUDIO 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/index)

[**KSTELEPHONY\_CALLCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol)

[**KSTELEPHONY\_CALLINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)

[**KSTELEPHONY\_PROVIDERCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)

[**KSTOPOLOGY\_ENDPOINTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointid)

[**KSTOPOLOGY\_ENDPOINTIDPAIR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)

[**LOOPEDSTREAMING\_POSITION\_EVENT\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

[**MDEVICECAPSEX**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-mdevicecapsex)

[**MIDIOPENDESC**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)

[**RTAUDIO\_GETREADPACKET\_信息**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt169891(v=vs.85))

[**RTAUDIO\_SETWRITEPACKET\_INFO**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt169892(v=vs.85))

[**SOUNDDETECTOR\_PATTERNHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**合成器\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_buffer)

[**合成器\_PORTPARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_portparams)

[**合成器\_统计信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_stats)

[**SYNTHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthcaps)

[**SYNTHDOWNLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthdownload)

[**SYNTHVOICEPRIORITY\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthvoicepriority_instance)

[**SYSAUDIO\_ATTACH\_VIRTUAL\_SOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**SYSAUDIO\_INSTANCE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_instance_info)

[**SYSAUDIO\_SELECT\_GRAPH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_select_graph)

[**UNCOMPRESSEDAUDIOFORMAT**](https://docs.microsoft.com/windows/desktop/api/audiomediatype/ns-audiomediatype-uncompressedaudioformat)

[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)

[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)
