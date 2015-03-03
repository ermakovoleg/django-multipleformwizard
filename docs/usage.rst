========
Usage
========

To use django-multipleformwizard in a project::

    # Every *WizardView that can be imported is an equivalent of a builtin *WizardView in Django
    from multipleformwizard import (SessionMultipleFormWizardView, CookieMultipleFormWizardView,
                                    NamedUrlSessionMultipleFormWizardView, NamedUrlCookieMultipleFormWizardView,
                                    MultipleFormWizardView, NamedUrlMultipleFormWizardView)
