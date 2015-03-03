========
Example Usage
========

How you could use django-multipleformwizard in a real-world situation::

    from __future__ import unicode_literals

    from django import forms
    from django.shortcuts import render_to_response

    from multipleformwizard import SessionMultipleFormWizardView

    from .forms import Form1, Form2, Form3

    class Wizard(SessionMultipleFormWizardView):
        form_list = [
            ("start", Form1),
            ("user_info", (
                ('account', Form2),
                ('address', Form3)
            )
        ]

        templates = {
            "start": 'demo/wizard-start.html',
            "user_info": 'demo/wizard-user_info.html'
        }

        def get_template_names(self):
            return [self.templates[self.steps.current]]

        def done(self, form_dict, **kwargs):
            result = {}

            for key in form_dict:
                form_collection = form_dict[key]
                if isinstance(form_collection, forms.Form):
                    result[key] = form_collection.cleaned_data
                elif isinstance(form_collection, dict):
                    result[key] = {}
                    for subkey in form_collection:
                        result[key][subkey] = form_collection[subkey].cleaned_data

            return render_to_response('demo/wizard-end.html', {
                'form_data': result,
            })
