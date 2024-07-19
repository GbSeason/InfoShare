# InfoShare

SELECT su.user_id,COUNT(pat.pick_user_id) AS 'taskAmount' FROM sys_user su
LEFT JOIN pes_business.pes_aggregate_task pat ON su.user_id = pat.pick_user_id AND pat.status IN (0,1) AND pat.deleted = 0
GROUP BY su.user_id



select
        ltap.WERKS plant, ltap.LGORT storage_Location, ltak.BDATU create_On, ltak.BZEIT create_On_Time,
        ltap.MATNR material, ltap.MAKTX material_Description, ltap.NSOLA target_qty, ltap.ALTME alternative_unit_of_measure,
        lfa1.NAME1 supplier, ltap.NLTYP dest_styp, ltap.NLBER dest_section, ltap.NLPLA dest_storage_Bin,
        ltap.VLTYP src_styp, ltap.VLBER src_section, ltap.VLPLA source_storage_Bin, ltap.TANUM transfer_order_number,
        ltap.TAPOS transfer_order_Item, marc.Z07MKTEXT1 short_text1,marc.Z07MKTEXT2 short_text2,
        ltak.TBNUM tr_number, ltak.BETYP requirement_type, ltak.BENUM requirement_code, ltap.SOBKZ special_stock,
        ltap.WENUM goods_receipt_number, ltap.WEPOS goods_receipt_item, ltap.BESTQ stock_category, mseg.BUDAT_MKPF goods_receipt_date,
        ltak.BWLVS movement_type, lqua.VFDAT SLEDBBD, ltap.QPLOS inspection_lot_number, lqua.VERME available_stock
        From MARD_DALI_PT.LTAP_PPT ltap
        LEFT JOIN MARD_DALI_PT.LTAK_PPT ltak ON ltak.TANUM=ltap.TANUM
        LEFT JOIN MARD_DALI_PT.MARC_PPT marc ON marc.MATNR=ltap.MATNR and marc.WERKS=ltap.WERKS
        LEFT JOIN MARD_DALI_PT.MSEG_PPT mseg ON mseg.MBLNR= ltap.WENUM and mseg.ZEILE=ltap.WEPOS
        LEFT JOIN MARD_DALI_PT.LFA1_PPT lfa1 ON mseg.LIFNR=lfa1.LIFNR
        LEFT JOIN MARD_DALI_PT.LQUA_PPT lqua ON lqua.LQNUM=ltap.VLQNR AND lqua.WERKS=ltap.WERKS
        where
        ltap.LGNUM in ('56A','56C') and ltak.BWLVS IN ('319','999','983','935','952') and ltap.PQUIT=' '
