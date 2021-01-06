# FormCollapse

> 折叠面板，通常用在布局空间要求较高的表单场景
>
> 注意：只能用在 Schema 场景

## Markup Schema 案例

```tsx
import React from 'react'
import {
  FormCollapse,
  FormItem,
  Input,
  FormButtonGroup,
  Submit,
} from '@formily/antd'
import { FormProvider, createForm } from '@formily/react'
import { createSchemaField } from '@formily/react-schema-field'
import { Button, Form, Space } from 'antd'

const SchemaField = createSchemaField({
  components: {
    FormItem,
    FormCollapse,
    Input,
  },
})

const form = createForm()

export default () => {
  const formCollapse = FormCollapse.useFormCollapse()
  return (
    <FormProvider form={form}>
      <Form labelCol={{ span: 6 }} wrapperCol={{ span: 10 }}>
        <SchemaField>
          <SchemaField.Void
            title="折叠面板"
            x-decorator="FormItem"
            x-component="FormCollapse"
            x-component-props={{
              formCollapse,
            }}
          >
            <SchemaField.Void
              name="panel1"
              x-component="FormCollapse.CollapsePanel"
              x-component-props={{ header: 'A1' }}
            >
              <SchemaField.String
                name="aaa"
                title="AAA"
                x-decorator="FormItem"
                required
                x-component="Input"
              />
            </SchemaField.Void>
            <SchemaField.Void
              name="panel2"
              x-component="FormCollapse.CollapsePanel"
              x-component-props={{ header: 'A2' }}
            >
              <SchemaField.String
                name="bbb"
                title="BBB"
                x-decorator="FormItem"
                required
                x-component="Input"
              />
            </SchemaField.Void>
            <SchemaField.Void
              name="panel3"
              x-component="FormCollapse.CollapsePanel"
              x-component-props={{ header: 'A3' }}
            >
              <SchemaField.String
                name="ccc"
                title="CCC"
                x-decorator="FormItem"
                required
                x-component="Input"
              />
            </SchemaField.Void>
          </SchemaField.Void>
        </SchemaField>
        <FormButtonGroup.FormItem>
          <Button
            onClick={() => {
              form.query('panel3').void.get((field) => {
                field.setDisplay(field.display === 'none' ? 'visible' : 'none')
              })
            }}
          >
            显示/隐藏最后一个Tab
          </Button>
          <Button
            onClick={() => {
              formCollapse.toggleActiveKey('panel2')
            }}
          >
            切换第二个Tab
          </Button>
          <Submit onSubmit={console.log}>提交</Submit>
        </FormButtonGroup.FormItem>
      </Form>
    </FormProvider>
  )
}
```

## JSON Schema 案例

```tsx
import React from 'react'
import {
  FormCollapse,
  FormItem,
  Input,
  FormButtonGroup,
  Submit,
} from '@formily/antd'
import { FormProvider, createForm } from '@formily/react'
import { createSchemaField } from '@formily/react-schema-field'
import { Button, Form, Space } from 'antd'

const SchemaField = createSchemaField({
  components: {
    FormItem,
    FormCollapse,
    Input,
  },
})

const form = createForm()

const schema = {
  type: 'object',
  properties: {
    collapse: {
      type: 'void',
      title: '折叠面板',
      'x-decorator': 'FormItem',
      'x-component': 'FormCollapse',
      'x-component-props': {
        formCollapse: '{{formCollapse}}',
      },
      properties: {
        panel1: {
          type: 'void',
          'x-component': 'FormCollapse.CollapsePanel',
          'x-component-props': {
            header: 'A1',
          },
          properties: {
            aaa: {
              type: 'string',
              title: 'AAA',
              'x-decorator': 'FormItem',
              required: true,
              'x-component': 'Input',
            },
          },
        },
        panel2: {
          type: 'void',
          'x-component': 'FormCollapse.CollapsePanel',
          'x-component-props': {
            header: 'A2',
          },
          properties: {
            bbb: {
              type: 'string',
              title: 'BBB',
              'x-decorator': 'FormItem',
              required: true,
              'x-component': 'Input',
            },
          },
        },
        panel3: {
          type: 'void',
          'x-component': 'FormCollapse.CollapsePanel',
          'x-component-props': {
            header: 'A3',
          },
          properties: {
            ccc: {
              type: 'string',
              title: 'CCC',
              'x-decorator': 'FormItem',
              required: true,
              'x-component': 'Input',
            },
          },
        },
      },
    },
  },
}

export default () => {
  const formCollapse = FormCollapse.useFormCollapse()
  return (
    <FormProvider form={form}>
      <Form labelCol={{ span: 6 }} wrapperCol={{ span: 10 }}>
        <SchemaField schema={schema} scope={{ formCollapse }} />
        <FormButtonGroup.FormItem>
          <Button
            onClick={() => {
              form.query('panel3').void.get((field) => {
                field.setDisplay(field.display === 'none' ? 'visible' : 'none')
              })
            }}
          >
            显示/隐藏最后一个Tab
          </Button>
          <Button
            onClick={() => {
              formCollapse.toggleActiveKey('panel2')
            }}
          >
            切换第二个Tab
          </Button>
          <Submit onSubmit={console.log}>提交</Submit>
        </FormButtonGroup.FormItem>
      </Form>
    </FormProvider>
  )
}
```

## API

### FormCollapse

### FormCollapse.CollapsePanel

### FormCollapse.createFormCollapse

### FormCollapse.useFormCollapse