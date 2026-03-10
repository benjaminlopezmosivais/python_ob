<?xml version="1.0" encoding="utf-8"?>

<odoo>

  

    <record id="account.account_invoices" model="ir.actions.report">

        <field name="print_report_name">

            (object.name or '').replace('/','')

        </field>

    </record>

  

</odoo>